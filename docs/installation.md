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
- **Cloud:** Copy to the `\\Relay\plugins` directory on the Relay server.

## Install

To install the ACS FiservDNA connector, complete the following steps:

1. Download the ACS FiservDNA software from the SMA FTP site. The file is located at `/OpCon Releases/Integrations/FiservDNA/`. Select the required version.
2. Unzip the FiservDNA.zip file.
3. Based on your deployment type:
   - **On-prem:** Copy the FiservDNA directory to `\\SAM\plugins`. Restart the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
   - **Cloud:** Copy the FiservDNA directory to `\\Relay\plugins`. Restart the **SMA OpCon Relay** service.

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
