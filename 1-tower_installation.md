### Tower Installation (Single Node)

1) Find yourself a virtual machine. Stale inventory file listing VMs as follows:
```
[ec2]
ec2-54-221-38-82.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-221-38-82.compute-1.amazonaws.com
ec2-54-234-51-172.compute-1.amazonaws.com ansible_ssh_user=centos ansible_ssh_host=ec2-54-234-51-172.compute-1.amazonaws.com
ec2-184-72-175-22.compute-1.amazonaws.com ansible_ssh_user=ubuntu ansible_ssh_host=ec2-184-72-175-22.compute-1.amazonaws.com
ec2-54-221-145-181.compute-1.amazonaws.com ansible_ssh_user=ubuntu ansible_ssh_host=ec2-54-221-145-181.compute-1.amazonaws.com
```

2) SSH into your virtual machine. Format is as follows:
```
ssh centos@ec2-54-221-38-82.compute-1.amazonaws.com
```
* Notice that the user that you are SSH-ing in is dependent on your Linux distribution.

3) Elevate privileges:
```
sudo su -
```

4) Download the Ansible Tower tarball.
```
[root@ip-10-65-215-109 ~]# curl -LO http://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-latest.tar.gz
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 3761k  100 3761k    0     0  14.7M      0 --:--:-- --:--:-- --:--:-- 14.8M
```

5) Unpack the Tower tarball.
```
tar -zxvf ansible-tower-setup-latest.tar.gz 
```

6) Fill out the inventory file with `vi`.
* Press `:x` to save changes.
* Sample settings as follows:
```
[tower]
localhost ansible_connection=local

[database]

[all:vars]
admin_password='test'

pg_host=''
pg_port=''

pg_database='awx'
pg_username='awx'
pg_password='test'

rabbitmq_port=5672
rabbitmq_vhost=tower
rabbitmq_username=tower
rabbitmq_password='test'
rabbitmq_cookie=cookiemonster

# Needs to be true for fqdns and ip addresses
rabbitmq_use_long_name=false
```

7) Invoke `setup.sh` setup script:
```
./setup.sh -e "gpgcheck=0" -e "minimum_var_space=2" -e "pendo_state=off"
```
* Provide extra variables (an Ansible thing) to get this to work with our test systems.
* Bash part looks like this:
```
Loaded plugins: fastestmirror
epel-release-latest-7.noarch.rpm                                                                                                                                        |  14 kB  00:00:00     
Examining /var/tmp/yum-root-n85YLw/epel-release-latest-7.noarch.rpm: epel-release-7-9.noarch
Marking /var/tmp/yum-root-n85YLw/epel-release-latest-7.noarch.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package epel-release.noarch 0:7-9 will be installed
--> Finished Dependency Resolution

Dependencies Resolved
```

* Ansible part looks like this:
```
PLAY [tower:database] *************************************************************************************************************************************************************************

TASK [check_config_static : Ensure expected variables are defined] ****************************************************************************************************************************
skipping: [localhost] => (item=tower_package_name)  => {"changed": false, "item": "tower_package_name", "skip_reason": "Conditional result was False", "skipped": true}
skipping: [localhost] => (item=tower_package_release)  => {"changed": false, "item": "tower_package_release", "skip_reason": "Conditional result was False", "skipped": true}
skipping: [localhost] => (item=tower_package_version)  => {"changed": false, "item": "tower_package_version", "skip_reason": "Conditional result was False", "skipped": true}

TASK [check_config_static : Ensure at least one tower host is defined] ************************************************************************************************************************
skipping: [localhost] => {"changed": false, "skip_reason": "Conditional result was False", "skipped": true}

TASK [check_config_static : Ensure only one database host exists] *****************************************************************************************************************************
skipping: [localhost] => {"changed": false, "skip_reason": "Conditional result was False", "skipped": true}
```
