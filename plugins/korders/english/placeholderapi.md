---
description: PlaceholderAPI settings and KOrder placeholders.
icon: code
---

# PlaceholderAPI

## PlaceholderAPI

<a href="../placeholderapi.md" class="button secondary">Tiếng Việt</a> <a href="placeholderapi.md" class="button primary">English</a>

PlaceholderAPI is an **optional** integration. KOrder works normally without it.

```yaml
placeholderapi:
  enabled: true
  cache-millis: 3000
```

### Placeholders

| Placeholder                  | Result                               |
| ---------------------------- | ------------------------------------ |
| `%korder_version%`           | `R02-v2`                             |
| `%korder_author%`            | `V3rhs`                              |
| `%korder_ready%`             | `true` / `false`                     |
| `%korder_locale%`            | Current locale                       |
| `%korder_economy%`           | Economy provider                     |
| `%korder_economy_mode%`      | Economy mode                         |
| `%korder_gui%`               | Current GUI style                    |
| `%korder_active_orders%`     | Active, unexpired order count        |
| `%korder_has_active_orders%` | Whether the player has active orders |
| `%korder_stash%`             | `AVAILABLE` Stash entry count        |
| `%korder_has_stash%`         | Whether items await collection       |

Available aliases:

```
%korder_economy_provider%
%korder_gui_style%
%korder_orders%
%korder_stash_entries%
%korder_pending_deliveries%
```

Player-specific placeholders return `0` or `false` without a player.

Database placeholders use cached, asynchronous refreshes. KOrder does not run synchronous SQLite queries during scoreboard or TAB updates.

The cache is invalidated after relevant order or Stash changes. It clears on reload and disable.
