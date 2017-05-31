### Ansible Inventories
Inventories detail your hosts. A simple inventory file for localhost:
```
[local]
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'
```

A simple inventory file for an Amazon EC2 instance:
```
[tower]
ec2-54-163-151-45.compute-1.amazonaws.com ansible_ssh_user=ec2-user ansible_ssh_host=ec2-54-163-151-45.compute-1.amazonaws.com
```

A more complicated inventory file:
```
[all]
ec2-54-242-92-121.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-242-92-121.compute-1.amazonaws.com
ec2-54-160-173-131.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-160-173-131.compute-1.amazonaws.com

[ungrouped]

[ec2]
ec2-54-242-92-121.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-242-92-121.compute-1.amazonaws.com
ec2-54-160-173-131.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-160-173-131.compute-1.amazonaws.com

[ldap]
ec2-54-160-173-131.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-160-173-131.compute-1.amazonaws.com

[tower]
ec2-54-242-92-121.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-242-92-121.compute-1.amazonaws.com

[cloud]
ec2-54-242-92-121.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-242-92-121.compute-1.amazonaws.com
ec2-54-160-173-131.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-160-173-131.compute-1.amazonaws.com
```
* Brackets detail a group.
* `ansible_ssh_user`: the user with which to SSH into your instance.
* `ansible_ssh_host`: the host to connect to.
* Other variables may exist.

### Example
Create an inventory file that models a small web application.
* Should have the following groups: `webservers`, `databases`, `ldap`, and `tower`.
* Just use localhost for the actual entries.

```
[webservers]
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'

[databases]
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'

[ldap]
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'

[tower]
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'
```
