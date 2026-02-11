# Operation

Agent and Task definition are only supported through Solution Manager.

JORS access is also only supported through Solution Manager.

To configure agent and task definitions, the associated Batch Users, environment and Error Words scripts must be defined.

To activate the agent, a connection will be established to the Fiserv DNA Oracle Database. If the connection fails, the agent will be placed in the **DOWN** state.

To submit events, an associated Windows Agent must be provided as the ACS IMplementation does not support the MSGIN functionality.

The ACS implementation sets the required Environment Variables matching those provided by the Windows Agent in order for the ACS execution to function correctly.