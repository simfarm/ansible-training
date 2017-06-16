### Roles

Roles are sort of like a more-involved playbook. There are a few discrete parts:
* A playbook that calls the role.
* The role itself (a collection of files and directories).

Let's investigate the calling playbook:
```
---

- name: create new hires packet
  hosts: all
  gather_facts: no 
  roles:
    - role: new_hires
```
* Notice the `roles` section.
* You can call as many roles as you'd like.

Roles are a combination of directories and files. For the `new_hires` role, we have:
```
└── new_hires
    ├── tasks
    │   └── main.yml
    ├── templates
    │   ├── acceptance.j2
    │   ├── benefits.j2
    │   └── company.j2
    └── vars
        └── main.yml
```
* Ansible looks for roles in a few discrete places. In this repo, we have:
```
└── playbooks
    ├─  new_hires.yml
    ├─  ...
    └── roles
        └── new_hires
```
* In other words, we have a `roles` directory that is inside of our `playbooks` directory.
* `new_hires` is the name of our role and is a directory that contains more files and folders.
* Our directory structure is important. Ansible needs to know where to look for roles on your machine.

Ansible roles support other features besides `vars` and `templates`. To read more about roles, click [here](http://docs.ansible.com/ansible/playbooks_roles.html#roles).
