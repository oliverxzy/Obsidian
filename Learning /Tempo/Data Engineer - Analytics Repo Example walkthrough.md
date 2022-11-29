#### Summary

I am using an example to show a typical process of data engineering tickets, including related dependency, git push, testing, and deploy to the prod database.

The original Ticket (BI-838) is an ETL issue that is related to data pulling from Bamboo_API, and storing data in our GCP database. We previously defined the employee_number column as an Integer in the schema, however, right now employee numbers come in as alpha-number combination. Therefore, we need to change the column type for employee number from Integer to String.

#### Instructions
1.  change employee_number from Integer to String on Bamboo_Employees.py from data models folder
    -   (Since the Bamboo_Employees table in GCP right now has employee_number column as Integer, manually alter table in GCP will cause potential issue and should not allow.)
        ![[Pasted image 20221117194446.png]]
2.  apply DDLstatement for new data model to alter table
    1.  create ddl statement scripts under scripts folder ( scripts → ddls → [script file]).
        ![[Pasted image 20221117194514.png]]
    2.  import dependency (OperationName, DDLStatement), and your new data model (Bamboo_Employees)
        ![[Pasted image 20221117194520.png]]
    3.  Using DDLStatement function, and using correct parameters
        ![[Pasted image 20221117194537.png]]
3.  Run python -m utils.run_ddl_statements
    -   it will compare local repo with table_operations, then know which new ddl statements (ddls script we created above) need to run.
    -   Then, it will backup current table to temp dataset, and it will keep it for 30 days
    -   Finally, it will remove old related tables from both stage and data warehouse. and then create a new one based on changed data models
4.  Run python -m etl.employees.load_bamboo_employees to transform and load data into corrected table
    -   Since now we have a corrected empty bamboo_employees table, we will run load_bamboo_employees ETL to load data
5.  Commit to branch and create a Pull Request
6.  Run Analytics CD on test environment (Github)
    1.  select correct branch name and development environment
        ![[Pasted image 20221117194547.png]]
7.  Run Analytics CD on prod environment after PR closed
8.  Trigger related DAG on Airflow to update table ahead
    1.  For here, we need to run deployment_dag
        ![[Pasted image 20221117194555.png]]
    2.  Trigger DAG
	    ![[Pasted image 20221117194605.png]]