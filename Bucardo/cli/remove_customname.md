---
title: Bucardo remove customname
---

The **remove customname** command removes one or more custom name mappings from Bucardo's internal tables.

Example:

    # Removes the custom names with internal IDs of 1 and 4
    bucardo remove customname 1 4

Usage:

    bucardo remove customname <numbers>

The numbers are internal IDs that can be seen by issuing
the [list customname](/Bucardo/cli/list_customname) command.

### Internals

Removed custom names will cause a delete from the [customname table](/Bucardo/schema/customname).

### See also:

-   [add_customname](/Bucardo/cli/add_customname)
-   [list_customname](/Bucardo/cli/list_customname)
