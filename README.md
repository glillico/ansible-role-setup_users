# Ansible Role : setup_users

This role creates user accounts.

## Requirements

None.

## Role Variables

### defaults/main.yml

    setup_users_name
    
The username of the account, this is required.

    setup_users_comment
    
Set user description field.

    setup_users_state
    
Defines what do to with the account.

    setup_users_group
    
Defines the users primary group.

    setup_users_groups
    
Defines the users secondary groups.

    setup_users_shell
The shell to use for the user account.

    setup_users_password
    
Set the users password using.  This users an encrypted version of the password.

    setup_users_update_password
    
Should the users password be set evey time the playbook is run. Options are `always` or `on_create`, default is `always`.

    setup_users_password_lock
    
Should the password be locked.

    setup_users_home
    
The full path to user home directory.

    setup_users_create_home
    
Should the users home directory be created.

    setup_users_append
    
Should secondary groups be appended to existing ones or overwritten.

    setup_users_uid
    
The UID to use when creating the account.

    setup_users_remove
    
Should the users home directory be removed when state = absent.

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
