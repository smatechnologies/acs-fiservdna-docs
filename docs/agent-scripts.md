---
sidebar_label: 'Scripts'
title: Define FiservDNA scripts
description: "Instructions for creating the environment and error words scripts required by the ACS FiservDNA connector in the OpCon script library."
tags:
  - Procedural
  - System Administrator
  - Automation Engineer
---

# Define FiservDNA Scripts

**Theme:** Configure | **Audience:** System Administrator, Automation Engineer

## What is it?

The ACS FiservDNA implementation uses two scripts to provide the **environment.txt** and **SMAErrorWordsFile.txt** files for each task execution. These scripts are requested during the ACS agent definition and the contents of each script is passed during task startup to enable the creation of unique files for each task.

Use existing **environment.txt** and **SMAErrorWordsFile.txt** files from an existing FiservDNA legacy connector to provide the contents of each script.

## Define scripts

To define FiservDNA scripts, complete the following steps:

1.  Open Solution Manager.
2.  Select **Library**.
3.  Select **Scripts**.
4.  Select **Script Types** from the upper right-hand corner.
    1.  Select **+Add**.
    2.  In the **Name** field enter **Fiserv DNA**.
    3.  In the **File Extension** field enter **txt**.
    4.  In the **Description** field enter **Used for ACS FiservDNA Integration**.
    5.  Select **Save**.
5.  Select **Script Runners** from the upper right-hand corner.
    1.  Select **+Add**.
    2.  In the **Name** field enter **Fiserv DNA**.
    3.  In the **OS** field select **Fiserv DNA** from the list.
    4.  In the **Type** field select **Fiserv DNA** from the list.
    5.  In the **Command** field enter **cmd.exe /c**.
    6.  Select **Save**.
6.  Select **Scripts** from the upper right-hand corner.
    1.  Create the Connector.config script.
    2.  Select **+Add**.
    3.  In the **Name** field enter a name for the script. It is suggested using the proposed agent name and append **env** to the name.
    4.  In the **Type** field select **Fiserv DNA** from the list.
    5.  Assign the required roles.
    6.  In the **Script** field paste the contents of the **environment.txt** file.
    7.  Select **Save**.
7.  Select **Scripts** from the upper right-hand corner.
    1.  Create the Connector.config script.
    2.  Select **+Add**.
    3.  In the **Name** field enter a name for the script. It is suggested using the proposed agent name and append **errorwords** to the name.
    4.  In the **Type** field select **Fiserv DNA** from the list.
    5.  Assign the required roles.
    6.  In the **Script** field paste the contents of the **SMAErrorWordsFile.txt** file.
    7.  Select **Save**.
