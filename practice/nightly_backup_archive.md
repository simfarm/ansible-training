### Nightly Archive
You are a system administration who has been tasked with creating a playbook that will create nightly backups of an inventory of desktops. This time we want to create archives.
* The machines that you are trying to backup are the workstations for your company's media production team.
* We need to back up the `~/Documents`, `~/Pictures`, `~/Library`, `~/Movies`, `~/Music` directories.
* Perform the backup by using the **archive** module. Archived files should be stored under `/tmp/backup`.
* Ansible may take a long time to archive directory contents.

### Hint

```
---

- hosts: all
  gather_facts: false
  tasks:
    - name: create backup directory
      file:
        path: /tmp/backup
        state: directory
    - name: create an archive of Documents directory contents
      archive: 
        path: ~/Documents
        dest: /tmp/backup/documents.tar.bz2
        format: bz2
    - name: create an archive of Pictures directory contents
      archive:
        path: ~/Pictures
        dest: /tmp/backup/pictures.tar.bz2
        format: bz2
    << ADD HERE >>
```
