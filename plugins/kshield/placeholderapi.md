---
description: Placeholder `%kshield_*%` cho player, server, mod, check và event.
icon: code
---

# PlaceholderAPI

## PlaceholderAPI

KShield đăng ký expansion `%kshield_*%` khi PlaceholderAPI được cài.

### Player

```
%kshield_player%
%kshield_player_uuid%
%kshield_player_brand%
%kshield_player_version%
%kshield_player_ping_k%
%kshield_player_ping_t%
```

### Server

```
%kshield_server%
%kshield_version%
%kshield_api_version%
%kshield_platform%
%kshield_language%
%kshield_rule_count%
```

### Check

```
%kshield_check_name%
%kshield_check_description%
%kshield_check_violations%
%kshield_check_max_violations%
%kshield_check_debug%
```

### Mod

```
%kshield_mod%
%kshield_mod_id%
%kshield_mod_category%
%kshield_mod_reason%
%kshield_mod_list%
%kshield_blocked_mod_list%
%kshield_mod_count%
%kshield_blocked_mod_count%
%kshield_mod_action%
%kshield_mod_action_short%
%kshield_mod_detection_method%
%kshield_mod_detection_methods%
%kshield_mod_details%
%kshield_mod_event_id%
```

### Client và event

```
%kshield_client_type%
%kshield_bypass_status%
%kshield_session_state%
%kshield_mod_event_time%
%kshield_mod_event_late%
```

### Kiểm tra rule

```
%kshield_has_mod_Meteor%
```

Giá trị trả về là `true` hoặc `false`.

### Lý do kick

```yaml
kick-command: "kick %kshield_player% Mod: %kshield_blocked_mod_list%"
```

Không dùng `%kshield_mod_list%` nếu muốn bỏ các rule chỉ `LOG`.

`%tg_*%` vẫn là alias tương thích.
