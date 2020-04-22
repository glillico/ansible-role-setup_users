# Ansible Role : setup_users

This role creates user accounts.

## Requirements

None.

## Role Variables

### defaults/main.yml

    setup_users_name
    
Username, this is required

    setup_users_comment
    
Comment, default = none

    setup_users_state
    
State, default = present

    setup_users_group
    
Users primary group, default = {{ setup_users_name }}

    setup_users_groups
    
Users secondary groups, default = none

    setup_users_shell
    
Users shell, default = /bin/bash

    setup_users_password
    
Users encrypted password, default = none

    setup_users_update_password
    
Update_password option, default = on_create

    setup_users_password_lock
    
Lock password, default false, alse affected by the value of setup_users_update_password

    setup_users_home
    
User home directory, default = /home/{{ setup_users_home }}

    setup_users_create_home
    
Create users home directory, default = true

    setup_users_append
    
Should groups be appended to existing ones or overwritten, default = true

    setup_users_uid
    
UID to user when creating user

    setup_users_remove
    
Remove the users home directory when state = absent, default true

## Dependencies

None.

## Example Playbook

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - glillico.setup_users

## License

MIT

## Author Information

This role was created in 2020 by Graham Lillico.
