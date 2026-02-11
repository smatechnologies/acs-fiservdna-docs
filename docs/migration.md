# Legacy DNA to ACS DNA Migration
The conversion program provides a mechanism to migrate existing FiServ DNA legacy tasks to the new ACS Fiserv DNA environment.

One of the major changes is that all information for the task execution is now contained within the OpCon environment instead of residing in various files associated with each connector installation.

The previous .ini file contents are contained in the **Fiserv DNA** agent definition, while the environment and error word information are provided as scripts within the OpCon environment. 

All user information used is now selected from a list of Fiserv DNA Batch Users.

## Install Conversion Utilities
Download the ACS FiServ DNA migration software (ACSDNAMigration.zip) from the FTP site **/OpCon Releases/Integrations/FiservDNA/Migration Utility** and extract the ACSDNAMigration.zip file into a directory on a Windows system.

Edit the Conversion.config file setting the information using the **Encrypt.exe** utility to encrypt passwords and tokens.

```
[GENERAL]
DEBUG=OFF

[OPCON]
OPCON_API_ADDRESS=DESKTOP-QMQS7D3:443
OPCON_API_TOKEN=5a4459795a4749335a4749744e6a41354f433030595441344c546868596d51744d6a6b794d32457a4e4445345a574a6b
OPCON_PROFILE_NAME=OPCONXPS
OPCON_DB_SERVER=DESKTOP-QMQS7D3
OPCON_DB=opconxps
OPCON_DB_USER=sa
OPCON_DB_USER_PASSWORD=4d4842444d4735346343513d
OPCON_USER=ocadm
OPCON_USER_PASSWORD=6233426a6232353463484d3d

```

where

Property   |  Description
-------------------------- | ----------------
**[OPCON]**                | Header containing the name of the target OpCon system.
**OPCON_API_ADDRESS**      | The address and port number of the OpCon Rest-API
**OPCON_API_TOKEN**        | An OpCon application token encrypted using the Encrypt utility.
**OPCON_PROFILE_NAME**     | A profile name (default OPCONXPS).
**OPCON_DB_SERVER**        | The address of the OpCon Database server.
**OPCON_DB**               | The OpCon database name.
**OPCON_DB_USER**          | A database user that has the required privileges to interact with the OpCon database.
**OPCON_DB_USER_PASSWORD** | The password of the database user encrypted using the Encrypt utility.
**OPCON_USER**             | An OpCon user that has the required privileges to interact with the schedules.
**OPCON_USER_PASSWORD**    | The password of the OpCon user encrypted using the Encrypt utility.

## Encrypt.exe Utility
The Encrypt.exe utility uses standard 64 bit encryption to encrypt text strings. This utility must be used to encrypt passwords and tokens inserted into the Conversion.config file.

Arguments   |  Description
----------- | ----------------
**-v**      | The information to encrypt. If string includes special characters, placed double quotes around the string

Example on how to encrypt the value abcdefg

```
Encrypt.exe -v "abcdefg"

```

### CreateDNAAgent.exe Utility
The CreateDNAAgent.exe utility is used to create the ACS Agent definition that the tasks will use. 
The process creates the environment and error words scripts from the provided files used by the connector and then creates the agent definition. 
The agent name provided as one of the arguments is used to create the scripts (if agent name id DNA001, the environment file is converted to the 
DNA001_env script and SMAErrorWordsFile file is converted to the DNA001_errorWords script).

The process reads the environment and error words files creating the scripts, reads the Oracle connection file extracting the oracle database 
user and uses the SQL User provided by the -sur argument. The SQL User has been moved from the task definition to the agent definition. 
When defining arguments on the command line, if the argument contains spaces, enclose the argument in double quotes. 

Arguments   |  Description
----------- | ----------------
**-env**    | The name of the environment file that will be used to create the environment script.
**-err**    | The name of the error words file that will be used to create the error words script.
**-ini**    | The name of the .ini file that contains the connection information.
**-mmn**    | (Optional) The name of the Enhanced Monitoring machine name if not present in the files.
**-mn**     | The name of the ACS DNA agent to create.
**-oni**    | The name of the oracle file containing the e Oracle connection information.
**-opc**    | The name of target OpCon system (matches a header value in the Conversion.config file). 
**-sur**    | The SQL user name used to retrieve the Batch User the connection will use. 

Example on how to create an ACS DNA machine DNA001

```
CreateDNAAgent.exe -opc OPCON -mn DNA001 -env environment.txt -ini dnatest.ini -sur usrdna -oni "SMAOracleConnection 1.ini" -err SMAErrorWordsFile.txt

```

### ConvertDNATasks.exe Utility
The ConvertDNATasks.exe utility is used to convert existing Windows Fiserv DNA tasks within a schedule to new ACS Fiserv DNA tasks. 
The process scans through the schedule looking for Windows tasks and then if the Windows task has a job subtype of **Fiserv DNA** or the Windows Command Line contains **SMARunDNAJob**. 
If there is a match, a copy of the Windows properties is made, the task type is reset to a Null Job. The task type is changed to ACS / Fiserv DNA and then the Windows Command line is converted to the new ACS Fiserv DNA task and the ACS properties are then set into the task. The advantage of following this process is that existing definitions such as frequencies, dependencies, etc are not touched and remain as they were. Only the task data type is changed.

Arguments   |  Description
----------- | ----------------
**-jf**     | The job filter used to determine which tasks in the schedule should be converted (supports wildcards and a value of ALL indicates all Fiserv DNA tasks in the schedule must be converted).
**-mn**     | The name of the ACS agent that the task will be associated with.
**-opc**    | The name of target OpCon system (matches a header value in the Conversion.config file). 
**-sf**     | The schedule filter used to determine which schedules should be converted (supports wildcards and a value of ALL indicates all schedules must be converted).

Example on how to convert legacy Fiserv DNA tasks 

```
ConvertDNATasks.exe -opc OPCON  -mn DNA002 -sf DNATEST??V -jf ALL

```

## General Conversion Process
The first action is to create the Fiserv DNA Batch Users that the connector implementation requires. This includes the SQL and Oracle users.

The second action is to create the ACS Fiserv DNA Agent.

The third action is to convert legacy Fiserv DNA tasks to ACS Fiserv DNA.

### Create the required Batch Users

Using Solution Manager, create the required Batch Users (when creating the users, select **Fiserv DNA** from the target system drop-down list).
- Oracle User (from the connector SMAOracleConnection .ini file).
- SQL User (from the connector .ini file or the Legacy Fiserv DNA task definition).

### Create the ACS DNA Agent for the connection
This process requires the creation of the appropriate directory containing the various files needed during the agent creation process.

- create the environment script from the provided environment file.
- create the errorwords script from the provided errortwords file.
- extract the oracle connection information from the provided oracle connection file.
- extract the data from provided inin file.
- create the new Fiserv DNA Agent using the supplied name.
	- set the environment & errorwords script information
	- set the SQL and Oracle batch users.
	- set the arguments retrieved from the ini file.

### Convert the Legacy Fiserv DNA tasks
This process scans through the schedules and tasks converting the found according to the schedule and job filters. 
It is suggested that before starting the process, a copy of the OpCon database is made as well as a copy of the schedules to be converted.

The process resets the job data from Windows to ACS. No other OpCon objects such as frequencies, dependencies, events are touched. 

- create a directory consisting of the machine name in the **input-name** directory.
- copy the connector.ini, environment, SMAErrorWordsFile and SMAOracleConnection files into the created directory.
- run the createDNAAgent.exe utility using the appropriate arguments.
	- get the id associated with the target ACS Fiserv DNA agent.
	- retrieve a list of schedules according to the schedule filter.
	- process each selected schedule
		- get the list of master jobs associated with the schedule
		- check if the job is a Windows job.
		- check if the job-type is a Fiserv DNA job
		- if a Fiserv DNA job
			- get the Windows properties associated with the job
			- reset the job to a null job.
			- set the machine id and the machine type (27).
			- create the ACS properties object. 
			- convert the command line to Fiserv DNA job object.
			- commit the job changes.
