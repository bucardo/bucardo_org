---
title: Bucardo listen
---

Bucardo uses the LISTEN/NOTIFY system to communicate between processes (MCP, CTLs, and KIDs).

Items the [MCP](/Bucardo/MCP) listens for:

-   bucardo_mcp_ping
-   bucardo_activate_sync_\$syncname
-   bucardo_deactivate_sync_\$syncname
-   bucardo_reload_sync_\$syncname
-   bucardo_kick_sync_\$syncname
-   bucardo_mcp_fullstop
-   bucardo_mcp_reload
-   bucardo_reload_config
-   bucardo_log_message

Notices issued by the [MCP](/Bucardo/MCP):

-   bucardo_mcp_pong
-   bucardo_boot
-   bucardo_reload_config_finished
-   bucardo_reloaded_mcp
-   bucardo_nosyncs
-   bucardo_started
-   bucardo_stopped
-   bucardo_syncerror_\$syncname
-   bucardo_reload_config_finished
-   bucardo_reloaded_mcp
-   bucardo_reloaded_sync_\$syncname
-   bucardo_activated_sync_\$syncname
-   bucardo_deactivated_sync_\$syncname
-   bucardo_kick_\$syncname

Items the [CTL](/Bucardo/CTL) listens for:

-   bucardo_\$\$_ping
-   bucardo_kick_\$syncname
-   bucardo_syncdone_\$syncname_\$db

Notices issued by the [CTL](/Bucardo/CTL):

-   bucardo_\$\$_pong
-   bucardo_syncdone_\$syncname
-   bucardo_q_\$syncname_\$targetdb

Items the [KID](/Bucardo/KID) listens for:

-   bucardo_kid_\$\$_ping
-   bucardo_q_\$syncname_\$targetdb

Notices issued by the [KID](/Bucardo/KID):

-   bucardo_kid_\$\$_pong
-   bucardo_syncdone_\$syncname_\$targetdb
-   bucardo_synckill_\$syncname_\$targetdb
-   bucardo_synckill_\$syncname

