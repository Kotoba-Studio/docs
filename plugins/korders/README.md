---
description: Buy Order Marketplace cho máy chủ Minecraft Paper-family.
icon: envelope
---

# KOrder

## KOrder

<a href="./" class="button primary">Tiếng Việt</a> <a href="english/overview.md" class="button secondary">English</a> <a href="https://github.com/Kotoba-Studio/KOrder/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

KOrder là hệ thống **Buy Order** cho máy chủ Minecraft Paper-family.

Người mua tạo yêu cầu mua trước. KOrder giữ tiền trong escrow. Người khác giao đúng vật phẩm để nhận payout. Người mua nhận hàng qua **Delivery Stash**.

**Phiên bản:** R03v3\
**Tác giả:** V3rhs\
**Studio:** Kotoba Studio / K-Studio\
**Hỗ trợ:** [Discord](https://discord.gg/x9ScDT7fCV)

{% hint style="info" %}
Tiếng Việt là ngôn ngữ mặc định. Chọn **English** để xem bản tiếng Anh.
{% endhint %}

### Cài đặt và khởi động

#### KOrder dùng để làm gì?

KOrder phù hợp với SMP hoặc economy server cần thị trường mua tự động.

1. Buyer chọn item, số lượng và giá mỗi món.
2. KOrder giữ tổng tiền trong escrow.
3. Seller giao đúng item cho order.
4. Seller nhận payout.
5. Buyer nhận item qua Delivery Stash.

#### Yêu cầu

| Thành phần           | Yêu cầu                                    |
| -------------------- | ------------------------------------------ |
| Java                 | **21+**                                    |
| Server               | Paper / Folia / Canvas                     |
| Minecraft/Paper line | **1.21.1 → 26.2**                          |
| Economy              | Ít nhất một bridge hoặc provider hoạt động |
| Database             | SQLite được bundle trong plugin            |

KOrder khai báo `folia-supported: true`. Plugin dùng scheduler bridge cho callback gắn với player hoặc entity.

**Economy được hỗ trợ**

`economy.bridge` hỗ trợ các giá trị sau:

* `auto`
* `vaultunlocked`
* `vault`
* `playerpoints`
* `coinsengine`
* `excellenteconomy`

`auto` ưu tiên VaultUnlocked v2, sau đó Vault, rồi PlayerPoints trực tiếp.

KOrder có thể hook với Vault, VaultUnlocked, PlayerPoints, CoinsEngine, ExcellentEconomy, LuckPerms, PlaceholderAPI, Floodgate, Geyser-Spigot và ViaVersion. Chỉ economy provider đang sử dụng là bắt buộc.

#### Cài mới

1. Tắt hoàn toàn máy chủ.
2. Đặt `KOrder-R03v3.jar` vào thư mục `plugins/`.
3. Đảm bảo economy plugin đã cài và load bình thường.
4. Khởi động máy chủ.
5. KOrder tạo data folder, config, preset GUI, translations và SQLite database.
6. Chạy các lệnh sau:

```
/korder admin info
/korder admin doctor
```

Trạng thái mong muốn:

```
HEALTHY
```

Sau đó, chạy `/korder`. Tạo một order nhỏ, giao thử và claim stash trước khi vận hành production.

#### Nâng cấp từ R03 sang R03v3

R03v3 vẫn công khai version là `R03`. `v3` là build number.

1. Tắt hoàn toàn máy chủ.
2. Backup `plugins/KOrder/`.
3. Thay JAR cũ bằng `KOrder-R03v3.jar`.
4. Khởi động máy chủ.
5. Chạy `/korder admin doctor rescan`.
6. Chờ quét hoàn tất, rồi chạy `/korder admin doctor`.

{% hint style="info" %}
R03v3 thêm transaction journal và economy-provider binding. Active order cũ có thể là **legacy/unverified binding**. Đây là cảnh báo nguồn gốc dữ liệu. KOrder không tự xóa order.
{% endhint %}

#### File quan trọng

```
plugins/KOrder/config.yml
plugins/KOrder/korder.db
plugins/KOrder/items-vi.yml
plugins/KOrder/settings/
plugins/KOrder/translations/
```

`korder.db` lưu orders, escrow metadata, stash, economy ledger, audit và hardening tables. Không xóa database để sửa lỗi production.

Backup toàn bộ `plugins/KOrder/` sau khi tắt máy chủ hoàn toàn. Cách này tránh sao chép SQLite khi transaction đang commit.

#### Kiểm tra sau mỗi lần cập nhật

* `/korder admin info` hiển thị đúng economy provider.
* `/korder admin doctor` trả về `HEALTHY`.
* GUI, search, create, deliver và stash hoạt động đúng.
* Cancel hoàn lại phần escrow còn lại.
* Webhook test thành công nếu đã bật.

Nếu thao tác tiền hoặc item thất bại, không lặp lại transaction. Kiểm tra Doctor và pending ledger trước.

### Hướng dẫn người chơi

#### Mở marketplace

```
/korder
```

Aliases: `/order`, `/orders`, `/donhang`.

Tại GUI chính, người chơi có thể duyệt public orders, tìm kiếm, tạo order, xem order của mình, claim Delivery Stash và giao hàng.

#### Duyệt và tìm kiếm order

```
/korder browse
/korder browse <query>
/korder search <query>
```

`public` là alias nội bộ của `browse`. Search hỗ trợ username buyer, tên item tiếng Việt, tiếng Việt không dấu, Material tiếng Anh và aliases trong `items-vi.yml`.

```
/korder search kim cuong
/korder search diamond
/korder search Steve
```

KOrder tự chọn UI phù hợp:

1. **Native Dialog** trên client và server hỗ trợ Dialog API.
2. **Bedrock Form** khi Floodgate/Geyser khả dụng.
3. **Virtual Sign** cho Java client cũ.
4. **Anvil fallback** khi API chưa hỗ trợ virtual sign.

Virtual sign chỉ tồn tại phía client. Plugin không đặt block thật trong world.

#### Tạo Buy Order

**Tạo từ GUI catalog**

```
/korder create
```

Chọn item, số lượng, giá và xác nhận. Dialog UI mới dùng slider cho số lượng.

**Tạo từ item đang cầm**

```
/korder createhand <amount> <price>
```

Ví dụ: `/korder createhand 64 2500`.

KOrder clone item template với amount bằng `1`. Template này dùng để đối chiếu khi giao hàng.

**Tạo trực tiếp bằng Material**

```
/korder create <material> <amount> <price>
```

Ví dụ: `/korder create DIAMOND 64 2500`.

Tổng escrow bằng `số lượng × giá mỗi món`. Ví dụ, 64 Diamond × 2,500 bằng 160,000. Order chỉ được tạo khi economy và database transaction hợp lệ.

Mặc định:

```yaml
orders:
  default-limit: 3
  expiry-days: 7
  min-amount: 1
  max-amount: 2304
  min-unit-price: 1.0
  max-total-price: 100000000000.0
```

Permission rank có thể tăng số active orders.

#### Quản lý order của bạn

```
/korder mine
```

`/korder my` là alias. Từ **My Orders**, bạn xem tiến độ, tăng số lượng, hủy order và theo dõi trạng thái.

```
/korder add <id> <amount>
```

`increase` và `them` là aliases của `add`. KOrder chỉ tăng tới `orders.max-amount`. Tiền bổ sung được giữ bằng transaction riêng.

Hủy order tại **My Orders → Order Detail → Hủy đơn**. KOrder chỉ hoàn phần escrow còn lại.

#### Giao hàng cho người khác

1. Chạy `/korder browse`.
2. Chọn order.
3. Chọn item hợp lệ và số lượng.
4. Xác nhận giao.

Hoặc dùng:

```
/korder deliver <id> <amount>
/korder giao <id> <amount>
```

Khi `orders.exact-item-from-hand: true`, KOrder kiểm tra template đầy đủ. Lore, enchant hoặc metadata khác có thể làm item không khớp.

KOrder chặn AIR, item blacklist, overstack và item serialization quá lớn. Creative delivery bị chặn, trừ khi có bypass permission. Số lượng giao không thể vượt phần order còn thiếu. Order được kiểm tra lại khi commit.

#### Delivery Stash

```
/korder stash
/korder collect
```

Item seller giao luôn vào stash trước. Buyer không cần có inventory trống lúc giao hàng. Nếu inventory đầy khi claim, item chưa nhận vẫn nằm trong stash.

Nếu stash hiển thị đang khóa an toàn, không spam click. Chờ transaction kết thúc hoặc nhờ admin kiểm tra Doctor.

#### Trạng thái order

| Trạng thái  | Ý nghĩa                        |
| ----------- | ------------------------------ |
| `ACTIVE`    | Order còn mở và nhận giao hàng |
| `COMPLETED` | Đã giao đủ số lượng            |
| `CANCELLED` | Buyer đã hủy                   |
| `EXPIRED`   | Đã hết hạn                     |

Expiry mặc định là 7 ngày.

### Cấu hình và GUI

File chính là `plugins/KOrder/config.yml`. Sau khi sửa, chạy `/korder reload` hoặc `/korder admin reload`.

{% hint style="warning" %}
Reload chỉ tải lại cấu hình và ngôn ngữ KOrder. Không hot-unload plugin marketplace bằng PlugMan khi transaction đang hoạt động.
{% endhint %}

#### Language và update checker

```yaml
language: vi_VN
update-checker: true
```

Locales bundle sẵn: `vi_VN`, `en_US`, `es_ES`, `pt_BR` và `de_DE`.

Update checker chỉ thông báo release. Plugin không tự thay JAR. Translation nằm tại `plugins/KOrder/translations/`.

#### Economy

```yaml
economy:
  bridge: auto
```

Các mode hợp lệ: `auto`, `vaultunlocked`, `vault`, `playerpoints`, `coinsengine` và `excellenteconomy`.

Khuyến nghị dùng `auto`, trừ khi cần ép provider cụ thể. Order mới gắn với identity provider. Nếu provider thay đổi khi còn active escrow, KOrder có thể chuyển sang **DEGRADED / FAIL-CLOSED**.

Khi đổi economy plugin:

1. Kiểm tra active orders.
2. Backup database.
3. Đổi provider và restart.
4. Chạy `/korder admin doctor rescan`.
5. Chỉ mở marketplace khi Doctor hợp lệ.

#### GUI style

```yaml
gui:
  style: modern
```

Preset gồm `modern`, `king` và `custom`. Chúng nằm trong `plugins/KOrder/settings/`.

`modern` dùng page-size mặc định 45. `king` có bố cục order truyền thống. `custom` cho phép chỉnh title, slot, material icon, name, lore và direct-deliver behavior.

```yaml
gui:
  style: custom
```

```yaml
layout:
  page-size: 45
behavior:
  direct-deliver: true
```

`direct-deliver: true` mở flow giao hàng khi click order khác. Giá trị `false` mở detail page trước.

Slot `0..44` là vùng order/item. Slot `45..53` là thanh điều khiển. Material phải là Bukkit Material hợp lệ. Tên và lore hỗ trợ MiniMessage như `<#RRGGBB>`. Giữ nguyên placeholders như `{page}`, `{pages}` và `{order}`.

#### Search UI và Dialogs

```yaml
search:
  legacy-sign-fallback: true
  legacy-anvil-fallback: true
  bedrock-form: true
dialogs:
  enabled: true
  quantity-slider: true
  quantity-slider-width: 320
  quantity-slider-step: 1.0
  quantity-slider-label-format: '%s: %s'
```

Giữ ba fallback search ở `true` để tương thích tối đa. `quantity-slider` dùng slider trên client hỗ trợ Dialogs. KOrder feature-detect API mới và tự fallback trên nhánh 1.21.x cũ.

#### Orders, bảo mật và hiệu năng

```yaml
orders:
  default-limit: 3
  expiry-days: 7
  min-amount: 1
  max-amount: 2304
  min-unit-price: 1.0
  max-total-price: 100000000000.0
  allow-own-delivery: false
  exact-item-from-hand: true
```

`korder.limit.X` tăng giới hạn active orders. KOrder dùng giá trị lớn nhất giữa default và các permission limit của player.

`allow-own-delivery: false` ngăn buyer tự giao order của mình. `exact-item-from-hand: true` giữ item template chi tiết.

```yaml
security:
  action-lock-millis: 650
  reject-overstacked-items: true
  max-item-bytes: 262144
  audit-retention-days: 90
performance:
  io-threads: 4
  io-queue: 512
  search-cache: 256
  stash-claim-batch: 64
  expiry-batch: 8
  maintenance-seconds: 30
  audit-purge-batch: 1000
database:
  busy-timeout-ms: 1500
```

Giữ các giá trị hiệu năng mặc định khi bắt đầu. Chỉ tăng `io-threads` sau khi xác định I/O queue là bottleneck. SQLite dùng WAL và durability cao.

#### Item filters, broadcast và webhook

```yaml
allowed-items: []
blacklisted-items:
  - AIR
  - BARRIER
  - COMMAND_BLOCK
  - CHAIN_COMMAND_BLOCK
  - REPEATING_COMMAND_BLOCK
  - STRUCTURE_BLOCK
  - STRUCTURE_VOID
  - JIGSAW
  - DEBUG_STICK
```

`allowed-items: []` cho phép Material hợp lệ, trừ blacklist. Dùng whitelist để giới hạn chặt hơn.

```yaml
broadcast:
  enabled: true
discord-webhook:
  enabled: false
  url: ''
  username: KOrder
  avatar-url: ''
```

Broadcast chỉ áp dụng cho order mới. Webhook hỗ trợ `order-created`, `order-increased`, `order-delivered`, `order-completed`, `order-cancelled`, `order-expired` và `transaction-warning`.

Bật webhook rồi test bằng `/korder admin webhook test`. `transaction-warning` phù hợp cho kênh cảnh báo production.

`items-vi.yml` cho phép thêm display name và aliases:

```yaml
items:
  DIAMOND:
    display: 'kim cương'
    aliases: ['kim cuong']
```

### Permissions và integrations

#### Permissions

| Permission                              | Mặc định | Chức năng                        |
| --------------------------------------- | -------: | -------------------------------- |
| `korder.use`                            |     true | Dùng KOrder và mở marketplace    |
| `korder.create`                         |     true | Tạo order và tăng số lượng       |
| `korder.deliver`                        |     true | Giao item cho order              |
| `korder.admin`                          |       OP | Admin commands, reload và Doctor |
| `korder.update.notify`                  |       OP | Nhận thông báo update            |
| `korder.bypass.creative`                |       OP | Bypass creative-delivery guard   |
| `korder.limit.5` đến `korder.limit.200` |    false | Active order limit tương ứng     |

Nếu player có nhiều permission limit, KOrder dùng limit lớn nhất.

```
/lp group vip permission set korder.limit.10 true
/lp group mvp permission set korder.limit.30 true
```

#### Command reference

| Command                                      | Mô tả                                     |
| -------------------------------------------- | ----------------------------------------- |
| `/korder`                                    | Mở marketplace                            |
| `/korder help`                               | Xem trợ giúp                              |
| `/korder browse [query]`                     | Duyệt hoặc tìm public orders              |
| `/korder search <query>`                     | Tìm username hoặc item                    |
| `/korder create`                             | Mở catalog tạo order                      |
| `/korder create <material> <amount> <price>` | Tạo bằng Material                         |
| `/korder createhand <amount> <price>`        | Tạo theo item đang cầm                    |
| `/korder mine`                               | Xem order của mình                        |
| `/korder stash`                              | Mở Delivery Stash                         |
| `/korder collect`                            | Alias mở stash                            |
| `/korder deliver <id> <amount>`              | Giao trực tiếp                            |
| `/korder add <id> <amount>`                  | Tăng amount order                         |
| `/korder admin info`                         | Xem version, UI, economy, PAPI và webhook |
| `/korder admin pending`                      | Xem ledger chưa resolve                   |
| `/korder admin tx <id>`                      | Xem chi tiết transaction                  |
| `/korder admin doctor`                       | Xem Transaction Health                    |
| `/korder admin doctor rescan`                | Quét lại health                           |

Core aliases: `public → browse`, `my → mine`, `giao → deliver`, `increase/them → add`.

#### Economy, PlaceholderAPI và client integrations

Khi dùng `auto`, KOrder ưu tiên VaultUnlocked v2. Vault bridge hoạt động với mọi provider expose Vault Economy. PlayerPoints có direct bridge. CoinsEngine và ExcellentEconomy dùng mode tương ứng.

Không đổi provider khi còn active order mà chưa kiểm tra Doctor. Provider mismatch ngăn payout hoặc refund nhầm currency.

PlaceholderAPI identifier là `korder`.

| Placeholder                                      | Kết quả                  |
| ------------------------------------------------ | ------------------------ |
| `%korder_ready%`                                 | `true/false`             |
| `%korder_locale%`                                | Locale hiện tại          |
| `%korder_economy%` / `%korder_economy_provider%` | Economy provider         |
| `%korder_economy_mode%`                          | Bridge mode trong config |
| `%korder_gui%` / `%korder_gui_style%`            | GUI style                |
| `%korder_active_orders%` / `%korder_orders%`     | Active orders của player |
| `%korder_has_active_orders%`                     | `true/false`             |
| `%korder_stash%` / `%korder_stash_entries%`      | Số stash entries         |
| `%korder_pending_deliveries%`                    | Alias stash entries      |
| `%korder_has_stash%`                             | `true/false`             |

Database-backed placeholders dùng cache `placeholderapi.cache-millis` và refresh async. Giá trị có thể trễ vài giây. Không dùng `%korder_version%` trong scoreboard public cho đến khi metadata constants được đồng bộ.

Floodgate/Geyser dùng Bedrock Form khi `search.bedrock-form: true`. ViaVersion hỗ trợ môi trường client hỗn hợp. KOrder vẫn feature-detect Dialog và sign capability.

### Anti-dupe, Doctor và troubleshooting

#### Anti-dupe model

KOrder dùng nhiều lớp bảo vệ:

* SQLite transaction, WAL và durability cao.
* Economy ledger với transaction ID và trạng thái `PREPARED`.
* Per-player transaction fence và per-order action fence.
* Optimistic order `version` checks và revalidation trước commit.
* Item serialization, hash/fingerprint và overstack guard.
* Stash `AVAILABLE → CLAIMING`, unique `source_tx` và one-time Dialog tokens.
* R03v3 sidecar journal, economy provider binding và fail-closed health gate.

Mục tiêu là hành vi ownership và payout **at-most-once**. Không retry mù transaction marketplace.

#### Transaction journal và health

Journal R03v3 mirror economy ledger và audit state. Các phase gồm:

```
PREPARED
DB_COMMITTED
OWNERSHIP_COMMITTED
ECONOMY_SETTLED
STASH_COMMITTED
COMPENSATED
ABORTED
ATTENTION
```

Journal giúp Doctor phát hiện state drift. Không tự sửa journal hoặc database.

`HEALTHY` cho phép marketplace hoạt động. `DEGRADED / FAIL-CLOSED` chặn mutation mới để bảo toàn dữ liệu.

Các trigger gồm SQLite `quick_check` lỗi, escrow invariant sai, stash state bất hợp lệ, stale claim, orphan stash, unresolved ledger, journal drift, provider mismatch và runtime guard violation.

{% hint style="warning" %}
Khi trạng thái là DEGRADED, ưu tiên bảo toàn dữ liệu. Không ép marketplace hoạt động trở lại ngay.
{% endhint %}

#### Transaction Doctor

```
/korder admin doctor
/korder admin doctor rescan
```

Doctor kiểm tra SQLite, provider identity, active orders, legacy bindings, order invariants, stash states, stale claims, orphan stash, pending ledgers, provider mismatch và journal drift.

Với ACTIVE order:

```
escrow = (requested - fulfilled) × unit_price
```

Order không ACTIVE phải có `escrow = 0`. Doctor cũng kiểm tra requested, fulfilled, unit price và escrow không hợp lệ.

`AVAILABLE` không được có `claim_tx` hoặc `claim_started_at`. `CLAIMING` phải có cả hai giá trị.

#### Pending ledger và xử lý sự cố

```
/korder admin pending
/korder admin tx <tx-id>
```

Khi người chơi báo tiền hoặc item chưa xuất hiện, kiểm tra transaction ID trước. Không dùng `eco give` hoặc `eco take` trước khi xác định DB và provider state.

**Buyer bị trừ tiền nhưng không thấy order**

1. Ghi transaction ID nếu có.
2. Kiểm tra pending ledger và transaction detail.
3. Chạy Doctor.
4. Kiểm tra economy provider log.
5. Chỉ compensation sau khi xác nhận state.

**Seller giao item nhưng chưa nhận tiền**

1. Không yêu cầu seller giao lại.
2. Kiểm tra buyer stash và order fulfilled.
3. Kiểm tra ledger.
4. Xử lý theo evidence nếu ownership đã commit nhưng payout chưa confirmed.

**Buyer không claim được stash**

1. Kiểm tra chỗ trống inventory.
2. Mở lại `/korder stash`.
3. Nếu entry locked lâu, chạy Doctor.
4. Kiểm tra stale claims và pending transaction.

**Provider mismatch**

1. Dừng create, deliver và cancel mới.
2. Xác nhận provider đã tạo active orders.
3. Restore provider đó, hoặc giải quyết active escrow theo migration plan.
4. Rescan Doctor.

Không tiếp tục payout order Vault bằng PlayerPoints như cùng một currency.

#### Backup và lỗi thường gặp

Backup an toàn:

1. Tắt hoàn toàn máy chủ.
2. Copy toàn bộ `plugins/KOrder/`.
3. Giữ `korder.db`, config, settings và translations.

Không xóa `korder.db`, sửa SQLite khi server đang chạy, xóa journal cũ, reset `CLAIMING → AVAILABLE` tùy tiện hoặc hot-unload KOrder.

| Vấn đề                    | Kiểm tra                                                                   |
| ------------------------- | -------------------------------------------------------------------------- |
| Nền kinh tế chưa sẵn sàng | `/korder admin info`, economy plugin và `economy.bridge`                   |
| Order busy                | Chờ transaction trên order kết thúc                                        |
| Action busy               | Chờ player transaction fence được giải phóng                               |
| Dialog expired            | Mở lại flow từ `/korder`                                                   |
| Search không mở Dialog    | Đây có thể là fallback Dialog → Bedrock Form → Virtual Sign → Anvil        |
| Không giao được item      | Template, meta, amount, Creative, blacklist, overstack và `korder.deliver` |
| Stash đầy                 | Dọn inventory rồi claim lại                                                |

#### Production checklist

* [ ] Economy provider đúng.
* [ ] `/korder admin doctor` trả về `HEALTHY`.
* [ ] Backup gần nhất có thể restore.
* [ ] Create, partial delivery và full delivery đều pass.
* [ ] Cancel partial order refund đúng.
* [ ] Buyer stash claim và full-inventory behavior đều pass.
* [ ] Restart với active order pass.
* [ ] Webhook warning channel hoạt động nếu dùng.
* [ ] Không có PlugMan auto-reload KOrder.

Khi mọi mục đều pass, KOrder hoạt động theo flow của anti-dupe architecture.
