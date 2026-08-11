---
description: KOrder Buy Order Marketplace overview.
icon: house
---

# Overview

## KOrder

<a href="../" class="button secondary">Tiếng Việt</a> <a href="overview.md" class="button primary">English</a>

KOrder is a **Buy Order Marketplace** plugin for Paper-family Minecraft servers.

Players create buy orders and place funds in escrow. Other players deliver matching items for payment. Buyers collect delivered items from the Stash.

**Version:** R02-v2\
**Author:** V3rhs\
**Studio:** Kotoba Studio / K-Studio\
**Support:** [Discord](https://discord.gg/x9ScDT7fCV)

### Quick install

1. Stop the server. Do not hot-swap the JAR during active transactions.
2. Place `KOrder-R02-v2.jar` in `plugins/`.
3. Install a supported economy provider and start the server.
4. Update `plugins/KOrder/config.yml` if needed.
5. Run `/korder reload` after configuration changes.

### Compatibility

```
Paper / Leaf: 1.21 → 1.21.11
Paper / Leaf: 26.1 → 26.2
Folia / Canvas: scheduler-aware with compatible APIs
Plugin bytecode: Java 21
```

Spigot/Bukkit without the Paper scheduler API is not an official target.

KOrder avoids NMS and CraftBukkit. It routes Dialog, Anvil, and Bedrock forms by runtime capability.

{% hint style="warning" %}
The compact release JAR includes SQLite native support for Linux x86\_64 glibc only.

Rebuild for Windows, macOS, Linux ARM64, or Linux musl.
{% endhint %}
