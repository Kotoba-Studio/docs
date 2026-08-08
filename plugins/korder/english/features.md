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

Sellers can deliver part or all of the remaining quantity. The delivery GUI only selects a quantity. Items are removed only after **Confirm** and a transaction recheck.

### Order management

Active orders support:

* **Increase quantity** — keeps the unit price and adds escrow.
* **Cancel** — applies only to unexpired `ACTIVE` orders.
* Completed orders disappear from **My Orders** immediately.

### Stash

Delivered items remain in the Stash. Items that do not fit remain available for collection.

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

### Integrations

* PlaceholderAPI and Discord Webhook.
* Vault, VaultUnlocked, and PlayerPoints.
* CoinsEngine, ExcellentEconomy, Geyser, and Floodgate when available.
