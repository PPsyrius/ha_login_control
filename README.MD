# Login Control 

Custom Home Assistant component for clearing all tokens of specific user 

Usage:
1. Add `login_control:` to the configuration yaml of your HA instnace
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