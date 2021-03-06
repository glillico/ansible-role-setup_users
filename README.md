# Ansible Role : setup_users

[![CI](https://github.com/glillico/ansible-role-setup_users/workflows/CI/badge.svg)](https://github.com/glillico/ansible-role-setup_users/actions?query=workflow%3ACI)

This role creates groups and user accounts.

## Requirements

None.

## Role Variables

### defaults/main.yml

|Variable|Description|
|---|:---|
|suu_groups_create|Should groups be created.<br>(Options: `true`, `false`)|
|suu_groups_remove|Should groups be removed.<br>(Options: `true`, `false`)|
|suu_users_addorrm|Should users be created or removed.<br>(Options: `true`, `false`)|

#### Groups
|Variable|Description|
|---|:---|
|suu_groups_name|The name of the group, this is required.|
|suu_groups_gid|Set groups GID.|
|suu_groups_state|Defines if the group should be present or not.|

#### Users
|Variable|Description|
|---|:---|
|setup_users_name|The username of the account, this is required.|
|setup_users_comment|Set user description field.|
|setup_users_state|Defines if the account should be present or not.|
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

##### Create the group testgroup if it does not exist.
```
  - suu_groups_name: testgroup1
    suu_groups_gid: 7771
    suu_groups_state: present
```

##### Remove the group testgroup if it exists.
```
  - suu_groups_name: testgroup2
    suu_groups_gid: 7772
    suu_groups_state: absent
```

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

Created in 2020 by Graham Lillico.
