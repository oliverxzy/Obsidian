This document mainly to introduce datadog and related set up.

## Datadog API gateway Integration

### Set up the CloudWatch trigger for Datadog forwarder

We need set up log collection to enable API gateway logging into CloudWatch log groups. To Enable API Gateway logging:

1.  Go to API Gateway in your AWS console.
    
2.  Select the wanted API and go to the Stages section.
    
3.  In the **Logs** tab, enable **Enable CloudWatch Logs** and **Enable Access Logging**.
    
4.  Select the INFO level to make sure you have all the requests.
    
5.  Make sure your **CloudWatch Group** name starts with api-gateway.
    
6.  Select the JSON format (CLF and CSV are also supported) and add the following in the **Log format** box:
    

### Add CloudWatch trigger for Datadog forwarder lambda function

After we set up the The Datadog Lambda Function for send AWS Services Logs based on [https://docs.datadoghq.com/logs/guide/forwarder/](https://docs.datadoghq.com/logs/guide/forwarder/), we already have lambda function that can ships logs, custom metrics, and traces from environment to Datadog. The next step is to set up trigger for specific Cloudwatch log groups we want. Based on “Manually set up triggers section from [https://docs.datadoghq.com/logs/guide/send-aws-services-logs-with-the-datadog-lambda-function/?tab=awsconsole#manually-set-up-triggers](https://docs.datadoghq.com/logs/guide/send-aws-services-logs-with-the-datadog-lambda-function/?tab=awsconsole#manually-set-up-triggers):

1.  In the AWS console, go to **Lambda**.
    
2.  Click **Functions** and select the Datadog Forwarder.
    
3.  Click **Add trigger** and select **CloudWatch Logs**.
    
4.  Select the log group from the drop-down menu.
    
5.  Enter a name for your filter, and optionally specify a filter pattern. For the ticket [https://tempo-io.atlassian.net/browse/ML-422](https://tempo-io.atlassian.net/browse/ML-422) we want to monitor log groups:
    
    1.  API-Gateway-Execution-Logs_m1dx79jaw0/prod
        
    2.  /aws/sagemaker/Endpoints/lgb-ranker-snowflake-eap
        
    3.  /aws/sagemaker/Endpoints/issue-picker-2022-10-03-16-53-36-760
        
    4.  /aws/lambda/issue-lookup
        
    5.  /aws/lambda/issue-picker
        
6.  Click **Add**.
    
7.  Go to the [Datadog Log section](https://app.datadoghq.com/logs) to explore any new log events sent to your log group.
    

-   Below is the filter to find out each log groups on [Datadog Log section](https://app.datadoghq.com/logs):
    
    -   API-Gateway-Execution-Logs_m1dx79jaw0/prod:
        
        -   service:apigateway , Host: API-Gateway-Execution-Logs_m1dx79jaw0/prod
            
    -   API-Gateway-Execution-Logs_dvqrb7fknh/stage:
        
        -   service:apigateway , Host: API-Gateway-Execution-Logs_dvqrb7fknh/stage
            
    -   /aws/sagemaker/Endpoints/lgb-ranker-snowflake-eap
        
        -   service:cloudwatch , Host: /aws/sagemaker/Endpoints/lgb-ranker-snowflake-eap
            
    -   /aws/sagemaker/Endpoints/issue-picker-2022-10-03-16-53-36-760
        
        -   service:cloudwatch , Host: /aws/sagemaker/Endpoints/issue-picker-2022-10-03-16-53-36-760
            
    -   /aws/lambda/issue-lookup
        
        -   service:cloudwatch , Host: issue_picker_API_Gatway , resourcePath: /issue_lookup
            
    -   /aws/lambda/issue-picker
        
        -   service:cloudwatch , Host: issue_picker_API_Gatway , resourcePath: /issue_picker
            

## Datadog Walkthrough

### Create Dashboard and Widgets

A dashboard is Datadog’s tool for visually tracking, analyzing, and displaying key metrics, which enable you to monitor the health of your infrastructure.

To create a dashboard, click **+New Dashboard** on the [Dashboard List](https://docs.datadoghq.com/mobile/) page or **New Dashboard** from the navigation menu.

Basically, we have three most important types of widget can be added to dashboard for API gateway dashboard:

1.  Timeseries Widget (The timeseries visualization allows to display the evolution of one or more metrics, log events over time.)
    
2.  Query Value Widget (Query values display the current value of a given metric, APM, or log query.)
    
3.  Log Stream Widget (The Log Stream displays a log flow matching the defined query)
    

In the graphing editor, Functions can let you customize base on specific monitoring goal (Functions can be applied to your queries by clicking +).

Here is an example of how to apply an Exclusion function to exclude certain values of metric.

Here is an example of how to apply a timeshift function on your error logs to compare current data with data from one week before.

**For create Widgets that using Metrics**:

We can create Metrics that group by different resource. For example, we want to track total hits for issue_picker and issue_lookup using Timeseries widges:

-   Simply choose correct metrics: aws.apigateway.count based on resource:/issue_lookup or resource:/issue_picker
    

Then we can monitor both resource in the same plot:

**For creating Widgets that using Logs**:

For example we want get error logs list from issue-lookup:

-   Simply choose Log stream widget, and then choose Logs to graph data
    
-   make sure Host match the logs you want to track, and set status:ERROR
    

Then we can get latest error log from specific function:

## Datadog documentation reference

-   [https://docs.datadoghq.com/integrations/amazon_api_gateway/](https://docs.datadoghq.com/integrations/amazon_api_gateway/)
-   [https://docs.datadoghq.com/logs/guide/send-aws-services-logs-with-the-datadog-lambda-function/?tab=awsconsole](https://docs.datadoghq.com/logs/guide/send-aws-services-logs-with-the-datadog-lambda-function/?tab=awsconsole)
-   [https://docs.datadoghq.com/serverless/installation/python/?tab=custom](https://docs.datadoghq.com/serverless/installation/python/?tab=custom)
-   [https://docs.datadoghq.com/dashboards/widgets/log_stream/](https://docs.datadoghq.com/dashboards/widgets/log_stream/)
-   [https://docs.datadoghq.com/integrations/slack/?tab=slackapplication](https://docs.datadoghq.com/integrations/slack/?tab=slackapplication)