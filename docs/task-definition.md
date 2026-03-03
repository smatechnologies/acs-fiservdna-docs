# Task Definition

## Defining tasks

The FiservDNA implementation supports the following tasks:

Task Type                | Description
-------------------------|-------------------------------------
Run Fiserv DNA Job       | Executes a Fiserv DNA job on the Fiserv DNA Batch Server

Defining tasks only requires providing the values associated with the specific task. It is possible to use global properties when defining
tasks.

### Run Fiserv DNA Job Task


1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **Fiserv DNA** from the **Job Type** drop-down list.
    - Select **Run Fiserv DNA Job** from the **Task Type** drop-down list.

Enter details for Task Type **Run Fiserv DNA Job**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is a Fiserv DNA connection previously defined.
3.  In the **TaskConfiguration** section
    - **DNA Job Query** section can be used to fetch task information for a task defined in the Fiserv DNA environment and use this to populate the job OpCon Job information.
        - Select **Auto-Populate Values** to insert the returned values into the OpCon task definition.
        - Select **Replace Existing Values** to replace any existing values in the OpCon task definition.
        - In the **Query Name** field, enter the name of the task to retrieve from the Fiserv DNA environment. 
    - In the **Environment Variables** section enter the required properties.
        - In the **Schedule Date** field enter the name of the global property that contains the schedule date in the yyyyMMdd format or use the default and create the global property.
        - In the **Schedule Name** field use the default property.
        - In the **Job Name** field use the default property.
        - In the **Job Id** field use the default property.
    - In the **Job Configuration** section enter the required values.
        - In the **Application Name** field enter the name of the application to be processed.
        - In the **Application NUmber** field enter the application number - will override the application name field.
        - In the **Additional Parameters** section enter parameters associated with the job using "+ Add Item** button to add parameters to the list.
            - In the **Parameter Cd** field enter the parameter code.
            - In the **Parameter Value** field enter the parameter value.
        - In the **Additional Cyclic Parameters** section enter cyclic parameters associated with the job using "+ Add Item** button to add parameters to the list.
            - In the **Parameter** field enter the cyclic parameter.
        - If required, select **Cycle Code not Required**.
        - In the **Effective Date** field enter the effective date (use global properties to enter a $Schedule date value).
        - In the **Effective Date Offset** field enter the number of dates which will offset the effective date.
        - If required, select **Use Business Date**.
        - In the **Queue Number Property Name** field enter the name of an OpCon property that will be used to contain the jobs's queue number.
        - In the **Enhanced Monitoring** section, enter any monitoring information
            - In the **Max Seconds to Time-out** field enter the value that will fail the job in case of communications loss during status monitoring. 
            - If required, select **Fail on Inactivty**.
            - In the **Max seconds to execute** indicate the maximum number of seconds a job may execute before being marked as failed. 
        - In the **File Load** second
            - select **Enabled** if the job is a file load job.
            - In the **File Name** field enter the name of the file to load.
            - In the **Batch Count Property Name** enter the name of the OpCon property where the loaded batch count value will be stored.
            - In the **Record Count Property Name** enter the name of the OpCon property where the loaded record count value will be stored.  
            - In the **Credits Property Name** enter the name of the OpCon property where the loaded credit value will be stored.       
            - In the **Debits Property Name** enter the name of the OpCon property where the loaded debit value will be stored.  
            - In the **File Number Property Name** enter the name of the OpCon property where the loaded file number value will be stored.   
        - In the **Failure Criteria** section set the failure criteria for the OpCon task.
4.  Save the definition changes. 

