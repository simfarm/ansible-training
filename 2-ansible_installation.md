### Installing Ansible (on OSX)
1) Install Homebrew (an OSX package manager):
```
jcostiga-OSX:~ jcostiga$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
==> This script will install:
/usr/local/bin/brew
/usr/local/share/doc/homebrew
/usr/local/share/man/man1/brew.1
/usr/local/share/zsh/site-functions/_brew
...[truncated]...
```
2) Install Ansible using your newly-installed Homebrew:
```
jcostiga-OSX:~ jcostiga$ brew install ansible
==> Installing dependencies for ansible: readline, sqlite, gdbm, openssl, python, libyaml, openssl@1.1
==> Installing ansible dependency: readline
==> Downloading https://homebrew.bintray.com/bottles/readline-7.0.3_1.el_capitan.bottle.tar.gz
...[truncated]...
```

### Test Working Ansible
* Check `ansible` is responsive:
```
(tower-qa) Simfarm@chrwang-OSX:~/Git/tower-qa$ ansible --version
ansible 2.3.0.0
  config file = /Users/Simfarm/Git/tower-qa/ansible.cfg
  configured module search path = Default w/o overrides
  python version = 2.7.13 (default, Mar  1 2017, 14:12:32) [GCC 4.2.1 Compatible Apple LLVM 7.3.0 (clang-703.0.29)]
```
* Create an inventory file for localhost:
```
[local]
127.0.0.1 ansible_connection=local ansible_python_interpreter='/usr/bin/env python'
```
* Run an ad hoc command against localhost:
```
ansible -m setup 
```
* Create a test playbook:
```
---

- hosts: all
  gather_facts: false
  tasks:
    - ping:
```

* Run your test playbook:
```
(tower-qa) Simfarm@chrwang-OSX:~/Git/ansible-playbooks$ ansible-playbook -i inventory ping.yml 

PLAY [all] ************************************************************************************************************************************************************************************

TASK [ping] ***********************************************************************************************************************************************************************************
ok: [127.0.0.1]

PLAY RECAP ************************************************************************************************************************************************************************************
127.0.0.1                  : ok=1    changed=0    unreachable=0    failed=0 
```
