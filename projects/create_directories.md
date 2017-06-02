### Create Directories
You are a manager of a sales team and you have recently hired twelve new people. You now have twelve new computers to boostrap. On each laptop's desktop, you want the following directories:
* Invoices
* Contacts
* Travel expenses
* General expenses

### Hint
```
---

- hosts: all
  gather_facts: false
  tasks:
    - name: create invoices folder
      file:
        path: ~/Desktop/invoices
        state: directory
    - name: create travel expenses folder
      file:
        path: ~/Desktop/travel_expenses
        state: directory
    << ADD HERE >>
```
