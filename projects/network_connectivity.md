### Network Connectivity

You are tasked with writing a playbook to robustly check for the network connectivity of an inventory of hosts.
* Playbook should check for network connectivity using the "ping" module.
* To check for connection flakiness, invoke the ping module **five** times.
* Separate each ping invocation with a one second sleep. Use the **pause** module to do this.

### Hint
```
---

- hosts: all
  gather_facts: false 
  tasks:
    - name: ping
      ping: 
    - name: whatever
      pause:
        seconds: 1 
    << ADD HERE >>
```
