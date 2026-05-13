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

- **On-premises:** Copy to the `\\SAM\plugins` directory on the OpCon server.
  For On-premises customers, a remote SMANetCom should be installed on the Fiserv Batch server supporting
  the ACS FiservDNA Integration and a Windows Agent (to provide MSGIN capabilities). 
- **Cloud:** Copy to the `\\Relay\plugins` directory on the Relay server.
  For Cloud customers, SMARelay should be installed on the Fiserv Batch server supporting
  the ACS FiservDNA Integration and a Windows Agent (to provide MSGIN capabilities). 

## Install

To install the ACS FiservDNA connector, complete the following steps:

1. Download the ACS FiservDNA software from the SMA FTP site. The file is located at `/OpCon Releases/Integrations/FiservDNA/`. Select the required version.
2. Unzip the FiservDNA.zip file.
3. Based on your deployment type:
   - **On-prem:** Copy the FiservDNA directory to `\\SAM\plugins`. Restart the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
   - **Cloud:** Copy the FiservDNA directory to `\\Relay\plugins`. Restart the **SMA OpCon Relay** service.

## Install Remote SMANetCom on Fiserv Batch Server

1. Ensure that the batch server has SQL Server access to the OpCon database.
2. Define a name for the Netcom (i.e. Netcom_BSERV1)
3. Create a directory on the Batch server (i.e. c:\Netcom_BSERV1)
4. Copy the contents of the Opconxps\SAM directory of your OpCon Server (all dlls, config files, .JSON files and SMANetcom.exe)
5. Paste them into the directory you created (i.e. c:\Netcom_BSERV1).
6. Create a folder "Netcom_BSERV1" in \Programdata\opconxps\
7. Copy SMANetcom.ini and SMAODBCConfig.dat files from your OpCon Server Programdata\opconxps\SAM folder
8. Paste them into the created \Programdata\opconxps\Netcom_BSERV1
9. Edit the SMANetCom.ini file

   In the Service Settings section 
   - set the names to your new name (i.e Netcom_BSERV1)
   - set the RunMode to Service

   [Service Settings]
   ShortServiceName=Netcom_BSERV1
   DisplayServiceName=Netcom_BSERV1              # Name displayed in Services applet
   SMANetComName=Netcom_BSERV1
   RunMode=Service                               # Must be Managed or Service

10. Register service 
    - go to directory where netcom has been copied to (i.e. c:\Netcom_BSERV1) 
    - run the command SMANetCom.exe action:install
11. Go to Services and start the service Netcom_BSERV1
12. Go to Services and stop the service Netcom_BSERV1
13. go to \Programdata\opconxps\Netcom_BSERV1\plugins
14. Copy ACS software into this directory.
15. Go to Services and restart the service Netcom_BSERV1
16. Go to Services on OpCon server
    - stop SMA OpCon RestAPI service
    - stop SMA ServiceManager service
13. on the OpCon server, go to \Programdata\opconxps\SAM\plugins
14. Copy ACS software into this directory.
16. Go to Services on OpCon server
    - start SMA OpCon RestAPI service
    - start SMA ServiceManager service

Using Solution Manager configure your agent entering Netcom_BSERV in the Netcom definition.
## Upgrade

To upgrade the ACS FiservDNA connector, complete the following steps:

1. Download the ACS FiservDNA software from the SMA FTP site. The file is located at `/OpCon Releases/Integrations/FiservDNA/`. Select the required version.
2. Unzip the FiservDNA.zip file.
3. Based on your deployment type:
   - **On-prem:** Stop the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service. Copy the FiservDNA directory to `\\SAM\plugins`. Restart the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
   - **Cloud:** Stop the **SMA OpCon Relay** service. Copy the FiservDNA directory to `\\Relay\plugins`. Restart the **SMA OpCon Relay** service.

## FAQs

**Do I need to stop services before a fresh installation?**
No. For a fresh installation, copy the directory and then restart the relevant services. Stopping services first is only required for an upgrade.

**Where do I find the installation files?**
Download the ACS FiservDNA software from the SMA FTP site. The file is located at `/OpCon Releases/Integrations/FiservDNA/`.

**Does the installation location differ for on-premises and cloud deployments?**
Yes. On-premises deployments use the `\\SAM\plugins` directory. Cloud deployments use the `\\Relay\plugins` directory.
