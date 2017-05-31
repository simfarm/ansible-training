### Ad Hoc Commands
For when you want to execute an isolated task against a host.
* Uses the `ansible` command.
* `-m` for ansible module.
* `-a` for module arguments (see module documentation).

Ping localhost:
```
(tower-qa) Simfarm@chrwang-OSX:~/Git/tower-qa$ ansible all -i inventory -m ping
127.0.0.1 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

Gather facts:
```
(tower-qa) Simfarm@chrwang-OSX:~/Git/tower-qa$ ansible all -i inventory -m setup
127.0.0.1 | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
....
```

Install the apache webserver:
```
(tower-qa) Simfarm@chrwang-OSX:~/Git/tower-qa$ ansible all -i playbooks/inventory-vmfusion.py -m yum -a "name=httpd state=present" -u root
172.16.239.132 | SUCCESS => {
    "changed": true, 
    "msg": "Repository epel is listed more than once in the configuration\nRepository epel-source is listed more than once in the configuration\n", 
    "rc": 0, 
....
```
* `-u` for user, since only root can install packages on my host.
* Package names are different between Linux distributions.
* Different inventory here is simply a VMware virtual machine.

Install postgres:
```
(tower-qa) Simfarm@chrwang-OSX:~/Git/tower-qa$ ansible all -i playbooks/inventory-vmfusion.py -m yum -a "name=freeradius state=present" -u root
172.16.239.132 | SUCCESS => {
    "changed": true, 
    "msg": "Repository epel is listed more than once in the configuration\nRepository epel-source is listed more than once in the configuration\n", 
    "rc": 0, 
....
```

### Example
Use ad hoc commands to install a freeradius server on a Centos 6 virtual machine and start the freeradius service.

Install freeradius:
```
ansible all -i playbooks/inventory-vmfusion.py -m yum -a "name=freeradius state=present" -u root
```

Start freeradius:
```
ansible all -i playbooks/inventory-vmfusion.py -m service -a "name=radiusd state=started" -u root
```
* Many packages have services with different names. Here, our package is called `freeradius` and the underlying service is called `radiusd`.
