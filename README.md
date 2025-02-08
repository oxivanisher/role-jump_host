jump_host
=========
[![Ansible Lint](https://github.com/oxivanisher/role-jump_host/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/oxivanisher/role-jump_host/actions/workflows/ansible-lint.yml)

This role configures jump host things like:
* Ensuring a user specific user is present and configured
* Some packages are installed
* Clone the ansible repository
* Configure SSH server ports

Notes
-----

* The user groups for the jump host user are explicit. All additional groups will be removed.
* The SSH key will be stored in `.ssh/ansible_jump_host_git_clone_private_key`

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

| Name                            | Comment                                                            | Default value  |
|---------------------------------|--------------------------------------------------------------------|----------------|
| jump_host_ssh_port              | Additional (!) SSH port to be configured                           | `99922`        |
| jump_host_user_name             | User name for the jump host user                                   | `example`      |
| jump_host_user_comment          | Comment for the jump host user                                     | `John Doe`     |
| jump_host_user_groups           | Additional groups for the jump host user                           | `['adm','dialout','cdrom','sudo','audio','video','plugdev','games','input','netdev','spi','i2c','gpio','users']` |
| jump_host_ansible_repo          | The URL for the ansible repository to be cloned                    | `git@yourgitlab.tld:user/repo.git` |
| jump_host_ansible_location      | Where will the ansible repsitory be cloned to within the user home | `ansible`      |
| jump_host_git_clone_private_key | A SSH private key which is allowd to clone the repository          | `-----BEGIN OPENSSH PRIVATE KEY-----`<br>`Some SSH private key`<br>`-----END OPENSSH PRIVATE KEY-----` |

Example Playbook
----------------

```yaml
- name: Configure Jump Hosts
  hosts: jumphosts
  roles:
    - role: oxivanisher.linux_server.jump_host
      tags:
        - jump
```

License
-------

BSD

Author Information
------------------

This role is part of the [oxivanisher.linux_server](https://galaxy.ansible.com/ui/repo/published/oxivanisher/linux_server/) collection, and the source for that is located on [github](https://github.com/oxivanisher/collection-linux_server).
