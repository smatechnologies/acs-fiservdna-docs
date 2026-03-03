---
sidebar_label: 'Release Notes'
---

# FiservDNA ACS Release Notes

## General

When using the FiservDNA ACS implementation, the task becomes a wrapper for the Fiserv DNA Connector passing information when executing the connector. The various files (.ini, environment, error words) are created by the FiservDNA ACS environment for each task execution. User codes required for database access and drive mappings are defined as Fiserv DNA batch users.

A Fiserv DNA agent definition is required.
It is best to use the migration utilities to create the agent definition as the utility uses the various files (.ini, environment, error words) when creating the definitions and scripts (environment and error words files are stored as FiserDNA scripts).

As ACS does not provide a MSGIN capability, a standard Windows Agent must be installed alongside the ACS installation to provide MSGIN capabilities. 

## Release 25.0.3

**New Features**

:eight_spoked_asterisk: **CON-927**: Support Advnaced Failure Creteria.

**Bugs**

:eight_spoked_asterisk: **CON-885**: Drive mapping user passwords must be re-encrypted so the Fiserv DNA connector can decrypt them.
:eight_spoked_asterisk: **CON-886**: Implement Event definitions in the user interface and add them to the generated .ini file.
:eight_spoked_asterisk: **CON-919**: Support environment variables.

