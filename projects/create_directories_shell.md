### Create Directories
You are a manager of a sales team and you have twelve new computers to boostrap. On each laptop's desktop, you want the following directories:
* Invoices
* Contacts
* Travel expenses
* General expenses

This time however, you need to use the **shell** module instead of the **file** module.
* Run your playbook twice. What happens?

### Hint
```
---

- hosts: all
  gather_facts: false
  tasks:
    - name: create invoices folder
      shell: mkdir invoices
      args:
        chdir: ~/Desktop
    - name: create travel expenses folder
      shell: mkdir travel_expenses
      args:
        chdir: ~/Desktop
    << ADD HERE >>
```
