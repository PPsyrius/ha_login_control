[![hacs_badge][hacs_shield]][hacs]
[![GitHub Latest Release][releases_shield]][latest_release]

[hacs_shield]: https://img.shields.io/badge/HACS-Custom-41BDF5.svg?style=for-the-badge
[hacs]: https://github.com/hacs/integration

[releases_shield]: https://img.shields.io/github/release/PPsyrius/ha_login_control.svg?style=for-the-badge
[latest_release]: https://github.com/PPsyrius/ha_login_control/releases/latest

# HA Login Control 

Custom Home Assistant component for clearing all tokens of specific user 

## Installation
### *HACS*
If you want HACS to handle installation and updates, add ha_login_control as a custom repository.

## Usage
1. Add `ha_login_control:` to the configuration yaml of your HA instance
2. Get the User ID of the user that you want to clear (In HA, go to Configuration -> Persons -> Users -> Press on your user name. Window will open that will show your ID.)
3. Call `clear_refresh_tokens` service with `user_id` parameter with User ID that you retrieved in step 1.

## Example Code
- Force Guest Logout at 13:00 (Automation)
```yaml
- alias: 'Logout all guests at midnight'
  trigger:
    platform: time
    at: '13:00:00'
  action:
    service: token_control.clear_refresh_tokens
    data:
      user_id: [GUEST USER ID HERE]
```
- Force Logout (Manual Button)
```yaml
type: entities
entities:
  - entity: person.room160guest
  - entity: switch.guest_160_refresh_token
    type: button
    name: Room 160 Force Logout
    tap_action:
      action: call-service
      service: login_control.clear_refresh_tokens
      service_data:
        user_id: [GUEST USER ID HERE]
      target: {}
title: Guest Management
state_color: true
```