## Summary

This document aims to show the typical process of pushing additional data from the DW into Salesforce, including an ETL file change, git push, testing, testing on Salesforce Sandbox and deployment to the prod database.

The original ticket [https://tempo-io.atlassian.net/browse/BI-804](https://tempo-io.atlassian.net/browse/BI-804) is adding new fields about customer health score from the data warehouse to Salesforce. See detailed field descriptions on: [https://docs.google.com/spreadsheets/d/1zMaEV_Ljq3o8NfwOso3w3PzgGYIcNSUyTvBvfVOQHl0/edit#gid=1129839246](https://docs.google.com/spreadsheets/d/1zMaEV_Ljq3o8NfwOso3w3PzgGYIcNSUyTvBvfVOQHl0/edit#gid=1129839246)

## Instructions

1.  First of all, we need make sure our GCP contains enough data in our workspace own tables so that we can test if query can run without errors before pushing and creating PR. For BI-804, I’m missing data in both bi_ml and bi_dwh datasets. So for the code below 1. loading some data into Amplitude DWH table, 2. load ml table into my own dataset.
    
    1.  python -m etl.events.load_amplitude_cloud_events --start_time 20221013T14 --end_time 20221013T15
        
        python -m etl.events.load_amplitude_cloud_events --start_time 20221012T14 --end_time 20221012T15
        
        python -m etl.events.load_amplitude_cloud_events --start_time 20221011T14 --end_time 20221011T15
        
    2.  Then, following jobs need to be run in order to get some data in your new ML dataset:
        
        -   Training job: python -m ml.models.ts_cloud_training_generation
            
        -   Cloud jobs: python -m ml.models.ts_cloud_annual && python -m ml.models.ts_cloud_monthly
            
2.  Now we are trying to add new fields on etl.mappings.salesforce.bq_licenses.sql which later goes into Salesforce.
    
    -   Since we need join ts_cloud_churn_predictions for reference customer health score fields, we need to create a CTE.
        
    -   Also, since the ml_dataset has not been added as parameters for get_query_params before, we need assign a new variable (ml_dataset_name) to retrieve ML TableType from bigquery_dwh_info in APISyncHelper.py . And add ml_dataset_name to query_params for retrieve params.
        
3.  Commit to branch and create a Pull Request
    
4.  Run Analytics CD on test environment (Github)
    
    1.  select correct branch name and development environment
        
5.  Trigger the related Airflow DAGs on the test env (tempo-composer-test) for loading related data to Salesforce
    
    1.  For BI-804 we need ts_cloud_weekly_dag and salesforce_daily_dag
        
6.  After all the Airflow DAGs are finished, check Salesforce sandbox to see if data successfully been pushed
    
    1.  using search bar to search subscription_id that contains added fields data records
        
    2.  check if added fields exist in sandbox licenses
        
    3.  Following steps can check all fields setting in Licenses
        
        1.  go to setting → service setup
            
        2.  in the left sidebar, go to object manager
            
        3.  search “license” on quick find
            
        4.  click fields & relationships, then you can see all fields under licenses
            
    4.  after data checked, comment on tickets to let BI team know
        
7.  After BI team checked, merge PR to master and Run Analytics CD on Prod environment