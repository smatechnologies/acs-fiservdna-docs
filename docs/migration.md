---
sidebar_label: 'Migration'
title: Legacy DNA to ACS DNA migration
description: "Instructions for migrating existing Fiserv DNA legacy tasks to the ACS FiservDNA connector environment using the conversion utilities."
tags:
  - Procedural
  - System Administrator
---

# Legacy DNA to ACS DNA Migration

**Theme:** Build | **Audience:** System Administrator

## What is it?

The conversion program provides a mechanism to migrate existing Fiserv DNA legacy tasks to the new ACS Fiserv DNA environment.

One of the major changes is that all information needed to run a task is now contained within the OpCon environment instead of residing in various files associated with each connector installation.

The previous .ini file contents are contained in the **Fiserv DNA** agent definition, while the environment and error word information are provided as scripts within the OpCon environment.

All user information used is now selected from a list of Fiserv DNA Batch Users.

Use this migration process when you want to:
- Convert existing Windows Fiserv DNA jobs to ACS FiservDNA while preserving all frequencies, dependencies, and events.
- Move connector configuration from individual .ini files into the centralized OpCon environment.

## Prerequisites

Before running the conversion utilities, complete the following:
- Download and extract ACSDNAMigration.zip from the SMA FTP site at `/OpCon Releases/Integrations/FiservDNA/Migration Utility`.
- Make a backup copy of the OpCon database and the schedules to be converted.

## Install Conversion Utilities

Download the ACS Fiserv DNA migration software (ACSDNAMigration.zip) from the FTP site **/OpCon Releases/Integrations/FiservDNA/Migration Utility** and extract the ACSDNAMigration.zip file into a directory on a Windows system.

Edit the Conversion.config file to set the information. Use the **Encrypt.exe** utility to encode passwords and tokens.

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
**OPCON_API_TOKEN**        | An OpCon application token encoded using the Encrypt utility.
**OPCON_PROFILE_NAME**     | A profile name (default OPCONXPS).
**OPCON_DB_SERVER**        | The address of the OpCon Database server.
**OPCON_DB**               | The OpCon database name.
**OPCON_DB_USER**          | A database user that has the required privileges to interact with the OpCon database.
**OPCON_DB_USER_PASSWORD** | The password of the database user encoded using the Encrypt utility.
**OPCON_USER**             | An OpCon user that has the required privileges to interact with the schedules.
**OPCON_USER_PASSWORD**    | The password of the OpCon user encoded using the Encrypt utility.

## Encrypt.exe Utility
The Encrypt.exe utility encodes text strings. Use it to encode the passwords and tokens inserted into the Conversion.config file.

:::caution
Encoding is not encryption. Anyone who can read Conversion.config can decode the values it contains. Restrict access to the file.
:::

Arguments   |  Description
----------- | ----------------
**-v**      | The value to encode. If the string includes special characters, place double quotes around the string.

To encode the value abcdefg, run:

```
Encrypt.exe -v "abcdefg"

```

### CreateDNAAgent.exe Utility
The CreateDNAAgent.exe utility creates the ACS Agent definition that the tasks use.
The process creates the environment and error words scripts from the provided files used by the connector and then creates the agent definition. 
The agent name provided as one of the arguments is used to create the scripts (if the agent name is DNA001, the environment file is converted to the 
DNA001_env script and SMAErrorWordsFile file is converted to the DNA001_errorWords script).

The process reads the environment and error words files creating the scripts, reads the Oracle connection file extracting the oracle database 
user and uses the SQL User provided by the -sur argument. The SQL User has been moved from the task definition to the agent definition. 
When defining arguments on the command line, if the argument contains spaces, enclose the argument in double quotes. 

Arguments   |  Description
----------- | ----------------
**-env**    | The name of the environment file used to create the environment script.
**-err**    | The name of the error words file used to create the error words script.
**-ini**    | The name of the .ini file that contains the connection information.
**-mmn**    | (Optional) The name of the Enhanced Monitoring machine name if not present in the files.
**-mn**     | The name of the ACS DNA agent to create.
**-oni**    | The name of the oracle file containing the Oracle connection information.
**-opc**    | The name of target OpCon system (matches a header value in the Conversion.config file). 
**-sur**    | The SQL user name used to retrieve the Batch User the connection uses.

To create the ACS DNA machine DNA001, run:

```
CreateDNAAgent.exe -opc OPCON -mn DNA001 -env environment.txt -ini dnatest.ini -sur usrdna -oni "SMAOracleConnection 1.ini" -err SMAErrorWordsFile.txt

```

### ConvertDNATasks.exe Utility
The ConvertDNATasks.exe utility converts existing Windows Fiserv DNA tasks within a schedule to new ACS Fiserv DNA tasks.
The process scans through the schedule looking for Windows tasks and then if the Windows task has a job subtype of **Fiserv DNA** or the Windows Command Line contains **SMARunDNAJob**. 
If there is a match, a copy of the Windows properties is made, the task type is reset to a Null Job. The task type is changed to ACS / Fiserv DNA and then the Windows Command line is converted to the new ACS Fiserv DNA task and the ACS properties are then set into the task. The advantage of following this process is that existing definitions such as frequencies, dependencies, etc are not touched and remain as they were. Only the task data type is changed.

Arguments   |  Description
----------- | ----------------
**-jf**     | The job filter used to determine which tasks in the schedule should be converted (supports wildcards and a value of ALL indicates all Fiserv DNA tasks in the schedule must be converted).
**-mn**     | The name of the ACS agent that the task is associated with.
**-opc**    | The name of target OpCon system (matches a header value in the Conversion.config file). 
**-sf**     | The schedule filter used to determine which schedules should be converted (supports wildcards and a value of ALL indicates all schedules must be converted).

To convert the legacy Fiserv DNA tasks in the matching schedules to the ACS DNA machine DNA001, run:

```
ConvertDNATasks.exe -opc OPCON -mn DNA001 -sf DNATEST??V -jf ALL

```

## General Conversion Process
The first action is to create the Fiserv DNA Batch Users that the connector implementation requires. This includes the SQL and Oracle users.

The second action is to create the ACS Fiserv DNA Agent.

The third action is to convert legacy Fiserv DNA tasks to ACS Fiserv DNA.

### Create the required Batch Users

Using Solution Manager, create the required Batch Users (when creating the users, select **Fiserv DNA** from the target system list).
- Oracle User (from the connector SMAOracleConnection .ini file).
- SQL User (from the connector .ini file or the Legacy Fiserv DNA task definition).

### Create the ACS DNA Agent for the connection
This process requires the creation of the appropriate directory containing the various files needed during the agent creation process.

- create the environment script from the provided environment file.
- create the errorwords script from the provided errorwords file.
- extract the oracle connection information from the provided oracle connection file.
- extract the data from the provided .ini file.
- create the new Fiserv DNA Agent using the supplied name.
	- set the environment & errorwords script information
	- set the SQL and Oracle batch users.
	- set the arguments retrieved from the ini file.

### Convert the Legacy Fiserv DNA tasks
This process scans through the schedules and tasks converting the found according to the schedule and job filters. 
Before starting the process, make a copy of the OpCon database as well as a copy of the schedules to be converted.

The process resets the job data from Windows to ACS. No other OpCon objects such as frequencies, dependencies, events are touched. 

To convert legacy Fiserv DNA tasks, complete the following steps:

1. Create a directory consisting of the machine name in the **input-name** directory.
2. Copy the connector.ini, environment, SMAErrorWordsFile and SMAOracleConnection files into the created directory.
3. Run the CreateDNAAgent.exe utility using the appropriate arguments. See [CreateDNAAgent.exe Utility](#creatednaagentexe-utility).
4. Run the ConvertDNATasks.exe utility using the appropriate arguments. See [ConvertDNATasks.exe Utility](#convertdnatasksexe-utility).

ConvertDNATasks.exe finds the target ACS Fiserv DNA agent and retrieves the schedules that match the schedule filter. In each selected schedule, it checks every master job. For each Windows job with the Fiserv DNA job type, it reads the job's Windows properties, resets the job to a null job, assigns the job to the ACS Fiserv DNA agent, converts the command line into the Fiserv DNA job definition, and saves the job.

## FAQs

**Are existing frequencies, dependencies, and events preserved during migration?**
Yes. No OpCon objects such as frequencies, dependencies, and events are touched during the conversion. Only the task data type is changed.

**Do I need to back up the database before converting?**
Yes. Before starting the conversion process, make a copy of the OpCon database and the schedules to be converted.

**Can I convert all tasks in all schedules at once?**
Yes. Use a value of `ALL` for both the schedule filter (`-sf`) and job filter (`-jf`) arguments when running ConvertDNATasks.exe.

**Do I still need to maintain .ini files on the remote server after migration?**
No. After migration, all configuration is contained within the OpCon environment. There is no longer any requirement to maintain configuration files on the remote server.

## Glossary

**Conversion.config** — The configuration file for the ACS DNA Migration utilities, containing connection settings for the target OpCon system including API address, database credentials, and user credentials.

**Job filter** — A pattern passed to ConvertDNATasks.exe via the `-jf` argument that determines which tasks within a schedule are converted. Supports wildcards; a value of `ALL` converts all Fiserv DNA tasks in the schedule.

**Schedule filter** — A pattern passed to ConvertDNATasks.exe via the `-sf` argument that determines which schedules are included in the conversion. Supports wildcards; a value of `ALL` converts all schedules.
