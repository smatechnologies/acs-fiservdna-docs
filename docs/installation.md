---
sidebar_label: 'Install and Upgrade'
title: Install and upgrade the ACS FiservDNA connector
description: "Step-by-step instructions for installing and upgrading the ACS FiservDNA connector on OpCon on-premises and cloud deployments."
tags:
  - Procedural
  - System Administrator
---

# Install and upgrade

**Theme:** Build | **Audience:** System Administrator

## What is it?

Install the ACS FiservDNA connector by copying the distribution directory to the correct location for your deployment type and restarting the relevant services. Upgrade follows the same process with an additional stop step before replacing the files.

- **On-premises:** Copy to the `\SAM\plugins` directory on the OpCon server.
  For On-premises customers, a remote SMANetCom should be installed on the Fiserv Batch server supporting
  the ACS FiservDNA Integration and a Windows Agent (to provide MSGIN capabilities).
- **Cloud:** Copy to the `\Relay\plugins` directory on the Relay server.
  For Cloud customers, SMARelay should be installed on the Fiserv Batch server supporting
  the ACS FiservDNA Integration and a Windows Agent (to provide MSGIN capabilities).

## Install

To install the ACS FiservDNA connector, complete the following steps:

1. Download the ACS FiservDNA software from the SMA FTP site. The file is located at `/OpCon Releases/Integrations/FiservDNA/`. Select the required version.
2. Unzip the FiservDNA.zip file.
3. Based on your deployment type:
   - **On-prem:** Copy the FiservDNA directory to `\SAM\plugins`. Restart the **SMA OpCon Service Manager** and **SMA OpCon RestAPI** services.
   - **Cloud:** Copy the FiservDNA directory to `\Relay\plugins`. Restart the **SMA OpCon Relay** service.
4. In Solution Manager, add an agent definition and confirm that **Fiserv DNA** appears in the **Type** list. If it does not, check that the FiservDNA directory is in the correct `plugins` directory and that the services were restarted. To finish the definition, see [Define the ACS FiservDNA Agent Connection](./agent-connection.md).

## Install Remote SMANetCom on Fiserv Batch Server

The example name used in these steps is `Netcom_BSERV1`. Replace it with the name you choose.

### Copy SMANetCom to the batch server

To copy SMANetCom to the Fiserv batch server, complete the following steps:

1. Ensure that the batch server has SQL Server access to the OpCon database.
2. Define a name for the NetCom, for example `Netcom_BSERV1`.
3. Create a directory on the batch server, for example `C:\Netcom_BSERV1`.
4. Copy the contents of the `Opconxps\SAM` directory of your OpCon server (all DLLs, configuration files, .JSON files and SMANetCom.exe).
5. Paste them into the directory you created, for example `C:\Netcom_BSERV1`.
6. Create a folder named `Netcom_BSERV1` in `\ProgramData\OpConxps\`.
7. Copy the SMANetCom.ini and SMAODBCConfig.dat files from the `\ProgramData\OpConxps\SAM` folder of your OpCon server.
8. Paste them into the folder you created, `\ProgramData\OpConxps\Netcom_BSERV1`.

### Configure and register the service

To configure and register the remote SMANetCom service, complete the following steps:

1. Edit the SMANetCom.ini file. In the `[Service Settings]` section, set the names to your new name and set `RunMode` to `Service`:

   ```ini
   [Service Settings]
   ShortServiceName=Netcom_BSERV1
   DisplayServiceName=Netcom_BSERV1              # Name displayed in Services applet
   SMANetComName=Netcom_BSERV1
   RunMode=Service                               # Must be Managed or Service
   ```

2. Go to the directory SMANetCom was copied to, for example `C:\Netcom_BSERV1`.
3. Run the command `SMANetCom.exe action:install` to register the service.
4. In Services, start the `Netcom_BSERV1` service.
5. In Services, stop the `Netcom_BSERV1` service.

### Copy the connector to the remote SMANetCom and the OpCon server

To copy the ACS software to both locations, complete the following steps:

1. On the batch server, go to `\ProgramData\OpConxps\Netcom_BSERV1\plugins`.
2. Copy the ACS software into this directory.
3. In Services, restart the `Netcom_BSERV1` service.
4. On the OpCon server, stop the **SMA OpCon RestAPI** and **SMA OpCon Service Manager** services.
5. On the OpCon server, go to `\ProgramData\OpConxps\SAM\plugins`.
6. Copy the ACS software into this directory.
7. On the OpCon server, start the **SMA OpCon RestAPI** and **SMA OpCon Service Manager** services.

In Solution Manager, configure your agent and enter `Netcom_BSERV1` as the NetCom name in the agent's **General Settings**. See [Define the ACS FiservDNA Agent Connection](./agent-connection.md).

## Upgrade

To upgrade the ACS FiservDNA connector, complete the following steps:

1. Download the ACS FiservDNA software from the SMA FTP site. The file is located at `/OpCon Releases/Integrations/FiservDNA/`. Select the required version.
2. Unzip the FiservDNA.zip file.
3. Based on your deployment type:
   - **On-prem:** Stop the **SMA OpCon Service Manager** and **SMA OpCon RestAPI** services. Copy the FiservDNA directory to `\SAM\plugins`. Restart the **SMA OpCon Service Manager** and **SMA OpCon RestAPI** services.
   - **Cloud:** Stop the **SMA OpCon Relay** service. Copy the FiservDNA directory to `\Relay\plugins`. Restart the **SMA OpCon Relay** service.
4. If you upgraded from a release earlier than 25.0.1, update each Fiserv DNA agent definition. The earlier **Error Words File** setting is cleared on upgrade because the field now takes a script.
   1. Open the agent definition in Solution Manager.
   2. In the **Error Words File** section select the error words script.
   3. Select **Save**.
5. In Solution Manager, confirm that **Fiserv DNA** still appears in the agent **Type** list.

## FAQs

**Do I need to stop services before a fresh installation?**
No. For a fresh installation, copy the directory and then restart the relevant services. Stopping services first is only required for an upgrade.

**Where do I find the installation files?**
Download the ACS FiservDNA software from the SMA FTP site. The file is located at `/OpCon Releases/Integrations/FiservDNA/`.

**Does the installation location differ for on-premises and cloud deployments?**
Yes. On-premises deployments use the `\SAM\plugins` directory. Cloud deployments use the `\Relay\plugins` directory.
