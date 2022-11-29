## Issue summary

The current situation is that based on issue [https://tempo-io.atlassian.net/browse/ML-304](https://tempo-io.atlassian.net/browse/ML-304) , we have 2 data pipeline AWS accounts:
-   tempo-datapipeline-staging-sso-administrators
-   tempo-datapipeline-prod-sso-administrators
    

we have a Slack integration to Airflow that Airflow can push success or failure message and error log (if it is a failed job) on both staging and prod environment.

We can successfully push both success and failure message for staging environment, but there is no failure message for prod environment. Both staging and prod sharing same data pipeline infrastructure, and same AWS set up. This document aim to diagnosis and solve this problem.

## Checked Comparison between Staging and Prod

1.  Permissions Policies
    
2.  SecretsManagerReadAccess
    
3.  Trusted entities (From Trust relationships)
    
4.  Revoke sessions
    
5.  Slack webhooks
    
6.  Test_slack_dag comparison step by step
    

## Testing process

To test in a different way, I start from replace post_slack_alert by customized function for both default_args and DAG()

### Make Prod Dag failed

Testing Prod update_variable.py

1.  For this step My update_variable.py look like this:
    

-   def test_slack_error_raise() that raise AirflowException('Error Message') error to make task failed
    
-   on_failure_callback=post_slack_alert in DAG to call post_slack_alert when dag failed
    

After we tested on prod env, there is no notification on Slack. And no failure message related to on_failure_callback in airflow log:

2. For this step My update_variable.py look like this:

-   def test_slack_error_raise() that raise AirflowException('Error Message') error to make task failed
    
-   'on_failure_callback': _alarm in default_args to showcase alarm that task is failed
    
-   Let on_failure_callback=_on_dag_run_fail in DAG to showcase that if DAG is failed
    

After we tested on prod env, there is still no notification on Slack. but both Task and Dag failure message successfully show up in log:

3. For this step My update_variable.py look like this:

-   def test_slack_error_raise() that raise AirflowException('Error Message') error to make task failed
    
-   'on_failure_callback': post_slack_alert in default_args to call post_slack_alert when Task failed
    
-   Let on_failure_callback=_on_dag_run_fail in DAG to showcase that if DAG is failed
    

After we tested on prod env, there is no notification on Slack. We get error message below when call post_slack_alert function.

Testing Stage update_variable.py

4. We are trying to replicate update_variable.py in Prod to Stage to see what is the error message.

-   def test_slack_error_raise() that raise AirflowException('Error Message') error to make task failed
    
-   'on_failure_callback': post_slack_alert in default_args to call post_slack_alert when Task failed
    
-   Let on_failure_callback=_on_dag_run_fail in DAG to showcase that if DAG is failed
    

update_variable_dag in Stag **can successfully push to slack**

5. The error raise on step 3. might cause by get_dag_start_time(context) function.

By calling Variable.get('dag_schedule', deserialize_json=True) in get_dag_start_time(context) from SlackHelper.py. We know that dag_schedules is a JSON format that:

```
{
"issues_dag":"5 4,16 * * *",
"worklogs_dag":"10 4,16 * * *",
"action_input_events_dag":"15 4,16 * * *",
"intent_input_events_dag":"20 4,16 * * *",
"suggestion_outcomes_dag":"25 4,16 * * *",
"task_suggestion_outcomes_dag":"30 4,16 * * *"
}
```

Which means whenever we call test_slack_dag or update_variable_dag , we end up getting NULL since they are not in dag_schedules info. And it wouldn’t trigger except KeyError to return context.get('dag_run').execution_date since dag_schedules exist.

6. For solve the issue we found above, we let get_dag_start_time(context) only do return context.get('dag_run').execution_date for testing update_variable_dag .

Finally we made Dag in Prod failed and push to slack now!

7. After Prod can successfully push failed notification to Slack, one other thing is to see if on_failure_callback can also call from DAG() level.

-   add on_failure_callback=post_slack_alert back in DAG()
    

Result: we also can get airflow failed notification on Slack

## Apply change to all Prod Airflow Jobs

### Change SlackHelper to make both Staging and Prod can push failed notification

Since we diagnosed the issue and successfully pushed failed notification to Slack only considering test dag. Next step is to apply changes to all Prod Airflow Jobs so that all of them can successfully push failed notification.

Original get_dag_start_time(context) just as below:

```
def get_dag_start_time(context):
    """
    Compute the start time of the current DAG run based on schedule and end date.

    :param context: Airflow context received from callback initiator.
    :type context: dict

    :return: DAG run start time
    :rtype: datetime
    """
    try:
        dag_schedules = Variable.get('dag_schedule', deserialize_json=True)
    except KeyError:
        # DAG schedules are not configured in the staging/test environment.
        # For ad hoc DAG runs, we use execution date because it is equivalent to start date
        #   since the value is set when the DAG is manually triggered.
        return context.get('dag_run').execution_date

    dag_id = context.get('task_instance').dag_id
    dag_schedule = dag_schedules.get(dag_id)

    # The last DAG start time is the most recent time from the schedule
    most_recent_run_time = croniter(dag_schedule).get_prev(datetime)
    dag_start_time = most_recent_run_time.replace(tzinfo=timezone('UTC'))

    return dag_start_time
```

**For the change we want**:

1.  make sure Staging and Prod environment share one logic
    
2.  When there is no schedules in the environment or dag is not been scheduled, return context.get('dag_run').execution_date
    
3.  When dag belongs to scheduled_dag in the environment, Compute the start time of the current DAG run based on schedule and end date.
    

-   Already Tested for test_slack_dag on Prod Environment but find out that dag_schedules = Variable.get('dag_schedule', deserialize_json=True) do not exist on Staging
    

Based on requirement and test above, New get_dag_start_time(context) as below:

```
def get_dag_start_time(context):
    """
    Compute the start time of the current DAG run based on schedule and end date.

    :param context: Airflow context received from callback initiator.
    :type context: dict

    :return: DAG run start time
    :rtype: datetime
    """
    try:
        dag_schedules = Variable.get('dag_schedule', deserialize_json=True)
    except KeyError:
        # DAG schedules are not configured in the staging/test environment.
        # For ad hoc DAG runs, we use execution date because it is equivalent to start date
        #   since the value is set when the DAG is manually triggered.
        return context.get('dag_run').execution_date

    dag_id = context.get('task_instance').dag_id

    if dag_id not in dag_schedules:
        # if the environment is Prod(do exist DAG schedules),
        # but current DAG not been scheduled, use execution date.
        return context.get('dag_run').execution_date
    dag_schedule = dag_schedules.get(dag_id)

    # The last DAG start time is the most recent time from the schedule
    most_recent_run_time = croniter(dag_schedule).get_prev(datetime)
    dag_start_time = most_recent_run_time.replace(tzinfo=timezone('UTC'))

    return dag_start_time
```

Tested on Both Staging and Prod environment. test_slack_dag on both env can successfully push failed notification to Slack!

### Find method to test if scheduled DAG in Prod can successfully push failed message

-   Added dag_schedules on the Staging airflow environment
    
-   Added JSON file that contain schedules for testing dag (test_slack_schedule_dag)
    
-   Created test_slack_schedule_dag for testing push failed notification in schedule
    

After that, we can successfully push failed notification on schedule for Staging environment.

### Created PR and Clean up testing files in both Staging and Prod

After we Created PR, and merged it to master. We have to clean up all testing files and code change we made for testing purpose. We will trigger Update Airflow S3 bucket for both Staging and prod as below:

For now, we already fixed the issue and successfully push it to staging and prod. The ticket now can be closed.