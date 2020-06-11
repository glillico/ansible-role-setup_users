# Ansible Role : setup_users

This role creates user accounts.

## Requirements

None.

## Role Variables

### defaults/main.yml

|Variable|Description|
|---|:---|
|setup_users_name|The username of the account, this is required.|
|setup_users_comment|Set user description field.|
|setup_users_state|Defines what do to with the account.|
|setup_users_group|Defines the users primary group.|
|setup_users_groups|Defines the users secondary groups.|
|setup_users_shell|The shell to use for the user account.|
|setup_users_password|Set the users account password using this encrypted version.|
|setup_users_update_password|Should the users password be set evey time the playbook is run.<br>(Options: `always` or `on_create`), (Default: `always`).|
|setup_users_password_lock|Should the password be locked.|
|setup_users_home|The full path to user home directory.|
|setup_users_create_home|Should the users home directory be created.|
|setup_users_append|Should secondary groups be appended to existing ones or overwritten.|
|setup_users_uid|The UID to use when creating the account.|
|setup_users_remove|Should the users home directory be removed when state = absent.|

#### Examples

##### Create this user account if it does not exist. Set the users shell to be /bin/bash.
```
  - setup_users_name: test1
    setup_users_comment: Test User 1
    setup_users_state: present
    setup_users_shell: /bin/bash
```

##### Remove this user account along with its home directory if it exists.
```
  - setup_users_name: test2
    setup_users_comment: Test User 2
    setup_users_state: absent
    setup_users_remove: true
```

##### Create this user account if it does not exist, and set the password every time the play book is run.
```
  - setup_users_name: test3
    setup_users_comment: Test User 3
    setup_users_state: present
    setup_users_shell: /bin/bash
    setup_users_password: $6$m.ALt.UnqqPruKDp$r86usNOcqm4hluHuYnjhMJ/LPDgpx4pYLlc40AciYq17GQDDgaIas3u0fXphx5vugxe3SQCzON7q6Mve4G4oh0
```

##### Create this user account if it does not exist, and set the password only when the account in created.
```
  - setup_users_name: test4
    setup_users_comment: Test User 4
    setup_users_state: present
    setup_users_shell: /bin/bash
    setup_users_password: $6$m.ALt.UnqqPruKDp$r86usNOcqm4hluHuYnjhMJ/LPDgpx4pYLlc40AciYq17GQDDgaIas3u0fXphx5vugxe3SQCzON7q6Mve4G4oh0
    setup_users_update_password: on_create
```

##### Create this user account if it does not exist, and set the password only when the account in created.
```
  - setup_users_name: test4
    setup_users_comment: Test User 4
    setup_users_state: present
    setup_users_shell: /bin/bash
    setup_users_password: $6$m.ALt.UnqqPruKDp$r86usNOcqm4hluHuYnjhMJ/LPDgpx4pYLlc40AciYq17GQDDgaIas3u0fXphx5vugxe3SQCzON7q6Mve4G4oh0
    setup_users_update_password: on_create
```

##### Create this user account if it does not exist. Sets the password to be locked.
```
  - setup_users_name: test6
    setup_users_comment: Test User 6
    setup_users_state: present
    setup_users_password_lock: true
```

##### Create this user account if it does not exist. Sets the users primary group to be staff.
```
  - setup_users_name: test7
    setup_users_comment: Test User 7
    setup_users_state: present
    setup_users_group: staff
```

##### Create this user account if it does not exist. Sets the users secondary group to be staff and users.
```
  - setup_users_name: test8
    setup_users_comment: Test User 8
    setup_users_state: present
    setup_users_groups: staff,users
```

##### Adds the secondary group of irc to an already exising user.
```
  - setup_users_name: test8
    setup_users_comment: Test User 8
    setup_users_state: present
    setup_users_groups: irc
    setup_users_append: true
```

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
