---
sidebar_label: 'Task Definition'
title: ACS FiservDNA task definition
description: "Instructions for defining FiservDNA tasks in OpCon Solution Manager, including Run Fiserv DNA Job task configuration."
tags:
  - Procedural
  - Automation Engineer
---

# Task Definition

**Theme:** Configure | **Audience:** Automation Engineer

## What is it?

The FiservDNA implementation supports the following tasks:

Task Type                | Description
-------------------------|-------------------------------------
Run Fiserv DNA Job       | Runs a Fiserv DNA job on the Fiserv DNA Batch Server

Defining tasks only requires providing the values associated with the specific task. It is possible to use global properties when defining tasks.

Use this page when you want to:
- Configure a Fiserv DNA batch job to run on a schedule managed by OpCon.
- Use DNA Job Query to import an existing Fiserv DNA task definition and auto-populate job fields, reducing manual entry.

## Prerequisites

An ACS FiservDNA agent connection must be defined and active before defining tasks. For instructions, see [Agent Definition](./agent-definition.md).

## Run Fiserv DNA Job Task

To add a master job definition, complete the following steps:

1.  Open Solution Manager.
2.  From the Home page select **Library**.
3.  From the **Administration** menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **Fiserv DNA** from the **Job Type** list.
    - Select **Run Fiserv DNA Job** from the **Task Type** list.

To configure task details for a Run Fiserv DNA Job task, complete the following steps:

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is a Fiserv DNA connection previously defined.
3.  In the **Task Configuration** section
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
        - In the **Application Number** field enter the application number - will override the application name field.
        - In the **Additional Parameters** section enter parameters associated with the job using **+ Add Item** button to add parameters to the list.
            - In the **Parameter Cd** field enter the parameter code.
            - In the **Parameter Value** field enter the parameter value.
        - In the **Additional Cyclic Parameters** section enter cyclic parameters associated with the job using **+ Add Item** button to add parameters to the list.
            - In the **Parameter** field enter the cyclic parameter.
        - If required, select **Cycle Code not Required**.
        - In the **Effective Date** field enter the effective date (use global properties to enter a $Schedule date value).
        - In the **Effective Date Offset** field enter the number of dates which will offset the effective date.
        - If required, select **Use Business Date**.
        - In the **Queue Number Property Name** field enter the name of an OpCon property that will be used to contain the job's queue number.
        - In the **Enhanced Monitoring** section, enter any monitoring information
            - In the **Max Seconds to Time-out** field enter the value that will fail the job in case of communications loss during status monitoring. 
            - If required, select **Fail on Inactivity**.
            - In the **Max seconds to execute** indicate the maximum number of seconds a job may execute before being marked as failed. 
        - In the **File Load** section
            - select **Enabled** if the job is a file load job.
            - In the **File Name** field enter the name of the file to load.
            - In the **Batch Count Property Name** enter the name of the OpCon property where the loaded batch count value will be stored.
            - In the **Record Count Property Name** enter the name of the OpCon property where the loaded record count value will be stored.  
            - In the **Credits Property Name** enter the name of the OpCon property where the loaded credit value will be stored.       
            - In the **Debits Property Name** enter the name of the OpCon property where the loaded debit value will be stored.  
            - In the **File Number Property Name** enter the name of the OpCon property where the loaded file number value will be stored.   
        - In the **Failure Criteria** section set the failure criteria for the OpCon task.
4.  Save the definition changes. 

## FAQs

**Must an agent connection exist before defining a task?**
Yes. An ACS FiservDNA agent connection must be defined and active before you can define tasks.

**Can I auto-populate task fields from an existing Fiserv DNA task definition?**
Yes. Use the **DNA Job Query** section to fetch task information from the Fiserv DNA environment. Select **Auto-Populate Values** to insert the returned values into the OpCon task definition.

**Can global properties be used in task definition fields?**
Yes. Global properties are supported when defining tasks.

**Does the Application Number field override the Application Name?**
Yes. Entering a value in the **Application Number** field will override the **Application Name** field.

## Glossary

**DNA Job Query** — A query sent to the Fiserv DNA environment to retrieve an existing task definition and pre-populate OpCon job fields.

**Effective Date** — The business date passed to the Fiserv DNA job. Supports global property substitution, such as `$SCHEDULE DATE`, and can be offset by a specified number of days using the **Effective Date Offset** field.
