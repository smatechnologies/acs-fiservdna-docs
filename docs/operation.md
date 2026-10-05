---
sidebar_label: 'Operation'
title: ACS FiservDNA connector operation
description: "Reference information for operating the ACS FiservDNA connector, including Solution Manager requirements, prerequisites, agent activation, and event submission."
tags:
  - Reference
  - System Administrator
  - Automation Engineer
---

# Operation

**Theme:** Overview | **Audience:** System Administrator, Automation Engineer

## What is it?

The ACS FiservDNA connector operates as an OpCon agent, activating when a connection to the Fiserv DNA Oracle database is established and submitting events through an associated Windows agent.

- The connector enters the **DOWN** state if the SMARunDNAJob program is missing or the Oracle database connection fails.
- All agent and task definitions, and JORS access, are only available through Solution Manager.

## Solution Manager

Agent and Task definition are only supported through Solution Manager.

JORS access is also only supported through Solution Manager.

## Prerequisites

To configure agent and task definitions, the associated Batch Users, environment and Error Words scripts must be defined.

## Agent activation

The connector communicates only when both of the following are true:

- The SMARunDNAJob.exe program is in the ACS FiservDNA connector directory.
- A connection to the Fiserv DNA Oracle database can be established.

The connector checks both conditions when the agent is activated and at every later status check. If either check fails, the agent is placed in the **DOWN** state.

## Submitting events

To submit events, an associated Windows Agent must be provided as the ACS implementation does not support the MSGIN functionality.

## Environment variables

The ACS implementation sets the environment variables that the Windows Agent provides, so that the Fiserv DNA job runs correctly. The values come from the **Environment Variables** section of the job definition. See [Task Definition](./task-definition.md).

Variable | Job definition field
-------- | --------------------
`SMA_MSLSAM_SCHEDULE_DATE` | **Schedule Date**
`SMA_MSLSAM_SCHEDULE_NAME` | **Schedule Name**
`SMA_MSLSAM_JOB_NAME` | **Job Name**
`SMA_MSLSAM_SAM_JOB_ID` | **Job Id**

## FAQs

**Why would an agent enter the DOWN state?**
The agent enters the DOWN state when the SMARunDNAJob.exe program is not in the connector directory, or when the connection to the Fiserv DNA Oracle database cannot be established. Both are checked at activation and at every status check.

**Does the ACS FiservDNA connector support the MSGIN functionality?**
No. An associated Windows agent must be provided to support MSGIN functionality and event submission.

**Can I define agents and tasks outside of Solution Manager?**
No. Agent and task definitions and JORS access are only supported through Solution Manager.
