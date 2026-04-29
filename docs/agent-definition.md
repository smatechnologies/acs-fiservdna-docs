---
sidebar_label: 'Overview'
title: ACS FiservDNA agent definition
description: "Overview of the ACS FiservDNA agent definition, including required batch users, scripts, and the agent connection configuration."
tags:
  - Conceptual
  - System Administrator
  - Automation Engineer
---

# Agent Definition

**Theme:** Configure | **Audience:** System Administrator, Automation Engineer

## What is it?

All definitions can only be performed using Solution Manager.

Once the ACS FiservDNA connector has been registered with the OpCon system, it will be possible to perform agent definitions.

One of the features of the ACS FiservDNA implementation is that all configuration data is maintained within the OpCon environment and the ACS FiservDNA implementation uses this information to create unique file instances for each execution.
- SMARunDNAJob.ini file
- SMAOracleConnection.ini file
- environment.txt file
- SMAErrorWordsFile.txt

The **environment.txt** file and the **SMAErrorWordsFile.txt** information are stored as FiservDNA scripts, while the information for the **SMARunDNAJob.ini** and **SMAOracleConnection.ini** files are defined when configuring the ACS FiservDNA connector.

The ACS FiservDNA implementation also makes use of OpCon batch users to provide the required user and passwords for the network drive mappings, the SQT user and the Oracle user inserted into the SMAOracleConfiguration.ini file.

Use this section when you want to:
- Configure the network drive mappings, SQT settings, Oracle connection, and processing options that apply to all jobs on this agent connection.
- Define this agent before defining individual tasks; tasks reference the agent connection by name.

## Configuration tasks

Complete these tasks in order before defining tasks:

1. [Define FiservDNA Batch Users](./agent-batch-users.md) — Create the OpCon batch users required for drive mappings, SQT, and Oracle authentication.
2. [Define FiservDNA Scripts](./agent-scripts.md) — Create the environment and error words scripts in the OpCon script library.
3. [Define the Agent Connection](./agent-connection.md) — Configure and activate the ACS FiservDNA agent in Solution Manager.

## FAQs

**Must batch users be defined before defining the agent?**
Yes. Batch users for each network drive mapping user, the SQT user, and the Oracle user must be defined before defining the agent connection.

**Must scripts be defined before defining the agent?**
Yes. The environment script and error words script must be created in the OpCon script library before defining the agent.

**Can global properties be used in agent definition fields?**
Yes. Global properties are supported in agent definition fields.

**What format should I use for OpCon properties in event templates?**
Use `<< >>` pairs instead of `[[ ]]` when defining OpCon properties in the **OpCon Event** field.

## Glossary

**Environment file** — A script stored in the OpCon script library that provides environment configuration to the Fiserv DNA connector at job runtime.

**Enhanced Monitoring** — An optional monitoring mode that tracks job status on a specified machine, with a configurable timeout and support for an additional error-checking program.

**SMAErrorWordsFile** — A script stored in the OpCon script library that provides the list of keywords monitored in job output; matching a keyword marks the job as failed.

**SMARunDNAJob** — The underlying program invoked by the ACS FiservDNA connector to run Fiserv DNA batch jobs.
