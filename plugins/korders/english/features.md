---
description: Buy orders, deliveries, Stash, UI styles, and integrations.
icon: sparkles
---

# Features

## Features

<a href="../chuc-nang.md" class="button secondary">Tiếng Việt</a> <a href="features.md" class="button primary">English</a>

### Buy orders

Buyers select an item, quantity, and unit price. KOrder validates the request before placing the total funds in escrow.

### Deliveries

Sellers can deliver part or all of the remaining quantity. The delivery GUI is a selection preview.

KOrder removes real items only after **Confirm**. It then rechecks the order and inventory under transaction guards.

### Order management

Active orders support:

* **Increase quantity** — keeps the unit price and adds escrow.
* **Cancel** — applies only to unexpired `ACTIVE` orders.
* Completed orders disappear from **My Orders** immediately.

### Stash

Delivered items remain in the persistent Stash. Items that do not fit remain available.

Claims reserve entries as `CLAIMING` before player data is saved. This favors no-dupe recovery after crashes.

### Interface styles

```
modern  — default, compact, and modern
king    — KingMC/Donut-style layout
custom  — custom text and layout
```

Presets are in `plugins/KOrder/settings/`:

```
modern.yml
king.yml
custom.yml
```

`custom.yml` owns its text across locale changes. Keep control slots unique and within `0..53`.

`page-size` is clamped to `9..45`. Stash always displays 45 entries per page.

### Search and input

KOrder prefers native Paper Dialog. Bedrock uses Floodgate/Geyser forms when available.

Unsupported Dialog paths use a virtual Anvil when enabled. R02-v2 never places temporary signs.

### Integrations

* PlaceholderAPI and Discord Webhook.
* Vault, VaultUnlocked v2, and PlayerPoints.
* CoinsEngine and ExcellentEconomy through Vault providers.
* Geyser and Floodgate when available.
