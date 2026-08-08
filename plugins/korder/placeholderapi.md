---
description: Placeholder và cấu hình cache cho PlaceholderAPI.
icon: code
---

# PlaceholderAPI

## PlaceholderAPI

<a href="placeholderapi.md" class="button primary">Tiếng Việt</a> <a href="english/placeholderapi.md" class="button secondary">English</a>

PlaceholderAPI là tích hợp **tùy chọn**. KOrder vẫn hoạt động bình thường khi không cài PlaceholderAPI.

```yaml
placeholderapi:
  enabled: true
  cache-millis: 3000
```

### Placeholder

| Placeholder                  | Kết quả                         |
| ---------------------------- | ------------------------------- |
| `%korder_version%`           | Phiên bản KOrder                |
| `%korder_author%`            | `V3rhs`                         |
| `%korder_ready%`             | `true` / `false`                |
| `%korder_locale%`            | Ngôn ngữ hiện tại               |
| `%korder_economy%`           | Economy provider                |
| `%korder_economy_mode%`      | Economy mode                    |
| `%korder_gui%`               | Style hiện tại                  |
| `%korder_active_orders%`     | Số đơn `ACTIVE` của người chơi  |
| `%korder_has_active_orders%` | Có đơn đang hoạt động hay không |
| `%korder_stash%`             | Số entry đang chờ trong Stash   |
| `%korder_has_stash%`         | Có hàng chờ nhận hay không      |

Alias có sẵn:

```
%korder_economy_provider%
%korder_gui_style%
%korder_orders%
%korder_stash_entries%
%korder_pending_deliveries%
```

Các placeholder liên quan database dùng cache và refresh bất đồng bộ. KOrder không query SQLite đồng bộ mỗi lần scoreboard hoặc TAB cập nhật.
