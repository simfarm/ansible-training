### Playbooks

* An Ansible script.
* Uses the `ansible-playbook` command.
* Basic invocation requires two arguments: an inventory file and a playbook.
* Sample playbooks [here](https://github.com/jlaska/ansible-playbooks).
* Run as follows:
```
ansible-playbook -i inventory playbook.yml
```

Sample playbook that will ping your all of your hosts:
```
---

- hosts: all
  gather_facts: false
  tasks:
    - ping:
```
* Hyphens up top denotate YAML.
* `hosts`: a host or group from your inventory file. Or something like "all": this will execute your playbook against all hosts.
* `gather_facts`: a setup task that gathers facts from your target host (what Linux distribution is this machine?). Fact variables may later be used in your playbook.
* `tasks`: list of ansible modules to call. Each module is basically one action to make.

Playbooks are supposed to be indempotent. This means that when you excecute a script twice, changes will only be made the first time.
* This is a HUGE advantage over bash scripts.
* Ansible is not fully idempotent in practice.

Here is a sample playbook that installs a RADIUS server and then restarts the RADIUS service:
```
---

- hosts: all
  gather_facts: true
  tasks:
    - name: Install FreeRADIUS packages
      yum:
        name: freeradius
        state: present
        update_cache: yes

    - name: Restart radius service
      service:
        name: radiusd
        state: restarted
        enabled: yes
```
* `name`: to help you remember what each task is about.
* Find out what flags you need by looking at our module documentation.
