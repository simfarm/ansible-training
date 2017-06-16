### Nightly Backup
You are a system administration who has been tasked with creating a playbook that will create nightly backups of an inventory of desktops.
* The machines that you are trying to backup are the workstations for your company's media production team.
* We need to back up the `~/Documents`, `~/Pictures`, `~/Library`, `~/Movies`, `~/Music` directories.
* Perform the backup by using the **copy** module to copy directory contents to `/tmp/backup`
* Ansible may take a long time to copy directory contents.

### Hint
```
---

- hosts: all
  gather_facts: false
  tasks:
    - name: copy documents
      copy:
        src: ~/Desktop
        dest: /tmp/backup/ 
    << ADD HERE >>
```
