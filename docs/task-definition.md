# Task Definition

## Defining tasks

The ACS Ease Connection supports the following task types:

Task Type                | Description
-------------------------|-------------------------------------
BUNDLE-RSJEDIT           | MONITOR and RSJEDIT tasks
BUNDLE-SEQ-FTP           | SEQ, COPY-RPT-OUT and RUN-FTP-OUT tasks
BUNDLE-SEQ-PROMPT        | SEQ and PROMPT tasks
COPY-DATA-TO-LTRFILE     | Copy outgoing Data File to Letter Files for FTP
COPY-RENAME-LTRFILE-OUT  | Copy or Rename Letter File for FTP
COPY-RPT-OUT             | Copy Report to Letter Files for FTP
FILEPERMS                | Update Letter File Privileges to 774
MONITOR                  | File Monitor for Incoming File       
MOVE-LTRFILE-TO-DATA     | Move incoming Letter File to Data Files
PROMPT                   | Answer a Single Prompt               
PROMPTSEQ                | Answer a Single Prompt with a SEQ    
RUN-FTP-OUT              | FTP Letter File off Symitar      
RENAME-LTRFILE-IN        | Rename Letter File Removing Prefix   
RESET                    | Reset a Single Prompt                
RSJ                      | Run Symitar Job (single-threaded)    
RSJEDIT                  | Runs Symitar Job with Edit File      
RSJMULTI                 | Run Symitar Job (multi-threaded)     
SEQ                      | Collect the SEQ of a Report  
SEQ-SEND                 | Copy Specified SEQ to Reports for FTP
TRANSLATE2COMMAS         | Answer a Single Prompt containing commas

Defining tasks only requires providing the values associated with the specific task. It is possible to use global properties when defining
tasks.

### BUNDLE-RSJEDIT Task


1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **BUNDLE-RSJEDIT : MONITOR and RSJEDIT tasks** from the **Task Type** drop-down list.

Enter details for Task Type **BUNDLE-RSJEDIT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the the name of the RSJ job associated with the RSJ task.
    - In the **Monitor File** field enter the monitor file name associated with the MONITOR task.
    - In the **Edit File** field enter the edit file name associated with the RSJ task.
4.  Save the definition changes. 

### BUNDLE-SEQ-FTP Task


1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **BUNDLE-SEQ-FTP : SEQ, COPY-RPT-OUT and RUN-FTP-OUT tasks** from the **Task Type** drop-down list.

Enter details for Task Type **BUNDLE-SEQ-FTP**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the the name of the RSJ job associated with the SEQ task.
    - In the **Output File** field enter the output file name associated with the COPY-RPT-OUT and RUN-FTP-OUT tasks.
    - In the **Email** field enter an email address that will receive notification when the transfer is complete.
4.  Save the definition changes. 

### BUNDLE-SEQ-PROMPT Task


1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **BUNDLE-SEQ-PROMPT : SEQ, and PROMPT tasks** from the **Task Type** drop-down list.

Enter details for Task Type **BUNDLE-SEQ-PROMPT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the the name of the RSJ job associated with the SEQ task.
    - In the **Prompt Job Name** field enter the name of the RSJ job associated with this PROMPTSEQ task.
    - In the **Prompt** field enter prompt to submit.
4.  Save the definition changes. 

### COPY-DATA-TO-LTRFILE Task


1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **COPY-DATA-TO-LTRFILE : Copy outgoing Data File to Letter Files for FTP** from the **Task Type** drop-down list.
    
Enter details for Task Type **COPY-DATA-TO-LTRFILE**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Source File** field enter the source file name associated with the task.
    - In the **Output File** field enter the output file name associated with the task.
4.  Save the definition changes. 

### COPY-RENAME-LTRFILE-OUT Task


1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **COPY-RENAME-LTRFILE-OUT : Copy or Rename Letter File for FTP** from the **Task Type** drop-down list.
    