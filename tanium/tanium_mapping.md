# Tanium Mapping

## Common Fields

| Data Field | ECS Field | Notes | 
| ---------- | --------- | ----- | 
| timestamp  | @timestamp | Timestamp of event as noted by Tanium |
| hostname   | host.hostname | |
| host       | host.ip | |
| tanium_computer_id | host.id | arguably, this should be independent of software agent and another internal ID |
| event | event.action | reported by tanium (e.g. `process_start`, `network_disconnect`) |


## `process_start` event-specific Fields

| Data Field | ECS Field | Notes | 
| ---------- | --------- | ----- | 
| fields.parent__command_line | process.parent.command_line | |
| fields.parent_pid | process.ppid | |
| fields.parent__file__full_path | process.parent.executable | |
| fields.command_line | process.command_line | | 
| fields.pid | process.pid | |
| fields.user__name | user.name | |
| fields.user__group | group.name | |
| fields.file__full_path | process.executable | |
| fields.file__md5 | file.hash.md5 | |
| fields.tanium_process_id | process.entity_id | | 
| fields.tanium_parent_process_id | process.parent.entity_id| |
| fields.create_time | process.start | |
