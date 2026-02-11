# Agent Definition

All definitions can only be performed using Solution Manager.

Once the sma.acs.FiservDNA plugin has been registered with the OpCon system, it will be possible to perform agent definitions.

One of the features of the ACS FiservDNA implementation is that all configuration data is maintained within the OpCon environment and the ACS FiservDNA implementation uses this information to create unique file instances for each execution.
- SMARunDNAJob.ini file
- SMAOracleConnection.ini file
- environment.txt file
- SMAErrorWordsFile.txt

The **environment.txt** file and the **SMAErrorWordsFile.txt** information are stored as FiservDNA scripts, while the information for the **SMARunDNAJob.ini** and **SMAOracleConnection.ini** files are defined when configuring the ACS FiservDNA connector.

The ACS FiservDNA implementation also makes use of OpCon batch users to provide the required user and passwords for the network drive mappings, the SQT user and the Oracle user inserted into the SMAOracleConfiguration.ini file.

Before defining an agent connection, the appropriate scripts and batch users should be defined.

## Defining FiservDNA Batch Users

The ACS FiservDNA integration requires the following batch users:
- Each user associated with a Network Drive Mapping.
- The SQT user.
- The Oracle User.

![Defining a Batch User](../static/img/fiservdna-batch-user.png)

1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Security*** Menu select **Batch Users**.
4.  Select **+Add** to add a new Batch User.
5.  Select **Fiserv DNA** from the ***Select the target OS*** drop-down list.
6.  Enter the User name that will be used to create the token in the **Identifier** field.
7.  Enter the password of the defined API User in the **Password** and **Confirm** fields.
8.  Select **Save**.

## Defining FiservDNA Scripts

The ACS FiservDNA implementation uses two scripts to provide the **environment.txt** and **SMAErrorWordsFile.txt** files for each task execution. These scripts are requested during the ACS agent definition and the contents of each script is passed during task startup to enable the creation of unique files for each task.

Use existing **environment.txt** and **SMAErrorWordsFIle.txt** files from an existing FiservDNA legacy connector to provide the contents of each script.

Using Solution Manager
- Select **Library**.
- Select **Scripts**.
- Select **Script Types** from the upper right hand corner. 
    - Select **+Add**
    - In the ***Name*** field enter **Fiserv DNA**.
    - In the ***File Extension field*** enter **txt**.
    - In the ***Description*** field enter **Used for ACS FiservDNA Integration**.
    - Select Save.
- Select **Script Runners** from the upper right hand corner. 
    - Select **+Add**
    - In the ***Name*** field enter **Fiserv DNA**.
    - In the ***OS*** field select **Fiserv DNA** from the drop-down list.
    - In the ***Type*** field select **AFiserv DNAS** from the drop-down list.
    - In the ***Command*** field enter **cmd.exe /c**.
    - Select Save.
- Select **Scripts** from the upper right hand corner.
    - Create the Connector.config script.
    - Select **+Add**.
    - In the ***Name*** field enter a name for the script. It is suggested using the proposed agent name and append **env** to the name. 
    - In the ***Type*** field select **Fiserv DNA** from the drop-down list.
    - Assign the required roles.
    - In the ***Script*** paste the contents of the **environment.txt** file.
    - Select Save.
- Select **Scripts** from the upper right hand corner.
    - Create the Connector.config script.
    - Select **+Add**.
    - In the ***Name*** field enter a name for the script. It is suggested using the proposed agent name and append **errorwords** to the name. 
    - In the ***Type*** field select **Fiserv DNA** from the drop-down list.
    - Assign the required roles.
    - In the ***Script*** paste the contents of the **SMAErrorWordsFIle.txt** file.
    - Select Save.

## Defining ACS Fiserv DNA Agent

The Agent definition defines the information that is included in the generated **SMARunJobDNA.ini** file.
 
This is done by adding a new ACS Fiserv DNA Agent definition using Solution Manager. 

Items defined in red are required values (note : global properties are supported). 

![Defining a Connection](../static/img/agent.png)

![Defining a Connection](../static/img/agent1.png)

![Defining a Connection](../static/img/agent2.png)

![Defining a Connection](../static/img/agent3.png)

![Defining a Connection](../static/img/agent4.png)

![Defining a Connection](../static/img/agent5.png)

![Defining a Connection](../static/img/agent6.png)

1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Agents**.
4.  Select **+Add** to add a new agent definition.
5.  Fill in the agent details
    - Insert a unique name for the connection.
    - Select **Fiserv DNA** from the **Type** drop-down list.
    - Select **General Settings**
    - Check that the NetCom Name is set to **Default** or the SMA Relay name if Relay is being used. 
    - Select **Fiserv DNA Settings**
    - In the **Network Drive Mappings** section enter the drive mappings.
        - In the **Drive Designation** field enter the letter assigned to the mapped drive.
        - In the **Share Name** field enter the address of the drive mapping.
        - In the **Drive User** field select the batch user to be used for the drive mapping.  
    - In the **Days to Keep Log files** field enter the vault indicating how long log files should be retained.  
    - In the **SQT Program Path** field enter the path to the SQT program which should be executed.  
   - In the **Environment File** section select the script containing the environment information.
   - In the **Base Directory** section enter the possible paths for SQT base directory.
    - Use the **+ AddItem** button to add values.
    - In the **SQT Configuration** section enter the SQT information.
        - In the **SQT User** field select the batch user to be used for SQT.  
        - In the **SQT Database** field enter the SQT database name.
        - In the **Override SQT Database** field enter the override SQT database name.
        - In the **SQT Report Path** field enter the expected directory for the generated SQT report file.
        - In the **SQT Response File Path** field enter the path to the directory where the response file will be generated.
        - If required, select **Generate SQT Error File details**.
        - In the **SQT Error File** field enter the template string.
    - In the **Oracle Configuration** section enter the information used to generate the SMAOracleConfiguration.ini file.
        - In the **Oracle User** field select the batch user to be used for the Oracle configuration.  
        - In the **Oracle DB Port** field enter the port on which the Oracle database is exposed.
        - In the **Oracle DB Service Name** field enter the service name of the Oracle database.
        - In the **Oracle DB Session Time-Out** field enter a time out value to use when connecting to the Oracle database.
    - In the **Job Start Event** section enter the information used to submit events to OpCon.
         - In the **Path To Msgin Directory** field enter the path to the msgin directory of the an associated Windows Agent.  
         - In the **OpCon User** field enter the OpCon user that will be used to submit the event.  
         - In the **OpCon User Password** field enter the external token of the OpCon user that will be used to submit the event.  
         - In the **OpCon Event** field enter the event template to be used. If OpCon properties are defined in the template definition use << >> pairs instead of [[ ]].  
    - In the **Enhanced Monitoring** section enter the enhanced monitoring information.
        - In the **Machine Name** field enter the name of the machine to use while monitoring.  
        - In the **Max seconds to Time-out** field enter the timeout value. 
        - If required, select **Use Additional Error Checking Program**.
        - In the **Additional Error Checking Program** field enter the path to an executable to perform  the additional error checking.  
        - In the **Error Checking Program Arguments** field enter arguments that will be passed to error checking program. 
    - In the **Error Words File** section select the script containing the error words file information.
    - In the **Processing Options** section enter the processing option information.
        - In the **Network Node Number** field enter the node number.  
        - If required, select **List Error Detail**.
        - In the **MSQUERR Threshold** field enter the number of errors in the error table to mark a job as failed.  
        - In the **Organization Number** field enter the organization number.  
        - In the **Default Parameter Date Format** field enter the default date definition.  
    - In the **Output File Handling** section enter the output file handling information.
        - If required, select **Copy Report to Output Directory**.
        - If required, select **Copy Report to Optical Directory**.
        - If required, select **Copy Report to Partner Directory**.
        - In the **Output Report Directory** field enter the directory information.  
        - If required, select **Use Distribution Ticket**.
        - In the **Optical Report Directory** field enter the directory information.  
6.  Save the definition changes. 
7.  Start the connection by selecting the **Change Communication Status** button and selecting **Enable Full Comm.**. 

