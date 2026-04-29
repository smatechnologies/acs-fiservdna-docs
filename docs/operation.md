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

- The connector enters the **DOWN** state if the Oracle database connection fails on activation.
- All agent and task definitions, and JORS access, are only available through Solution Manager.

## Solution Manager

Agent and Task definition are only supported through Solution Manager.

JORS access is also only supported through Solution Manager.

## Prerequisites

To configure agent and task definitions, the associated Batch Users, environment and Error Words scripts must be defined.

## Agent activation

To activate the agent, a connection will be established to the Fiserv DNA Oracle Database. If the connection fails, the agent will be placed in the **DOWN** state.

## Submitting events

To submit events, an associated Windows Agent must be provided as the ACS implementation does not support the MSGIN functionality.

## Environment variables

The ACS implementation sets the required Environment Variables matching those provided by the Windows Agent in order for the ACS execution to function correctly.

## FAQs

**Why would an agent enter the DOWN state?**
The agent enters the DOWN state when the connection to the Fiserv DNA Oracle database cannot be established during activation.

**Does the ACS FiservDNA connector support the MSGIN functionality?**
No. An associated Windows agent must be provided to support MSGIN functionality and event submission.

**Can I define agents and tasks outside of Solution Manager?**
No. Agent and task definitions and JORS access are only supported through Solution Manager.
