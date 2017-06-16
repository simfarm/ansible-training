### Playbooks Variables

Variables:
* Put at the top of your playbook.
* Denoted with double curly brackets:
```
---

- hosts: all
  gather_facts: false
  vars:
    user1: Jcostigan
    user2: Mbarry
    user3: Rfrankoff
  tasks:
    - name: create user1 folder
      file:
        path: ~/Desktop/{{user1}}
        state: directory
    - name: create user2 folder
      file:
        path: ~/Desktop/{{user2}}
        state: directory
    - name: create user3 folder
      file:
        path: ~/Desktop/{{user3}}
        state: directory
```

You can also pass in variables by the command line:
```
ansible-playbook -i inventory playbook.yml -e "user1=from_var" -e "user2=from_var2"
```
* Will now create folders called "from_var" and "from_var2."
* Variables given by command line will override variables defined at the top of your playbook.
* Ansible has additional variable precedence rules.
