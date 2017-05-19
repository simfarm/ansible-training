### Additional Resources
* Install [Sublime](https://www.sublimetext.com/) (text editor for code).
* Learn about the Unix filesystem. A good starting point contained [here](https://www.tutorialspoint.com/unix/unix-file-system.htm). (Learning this - spend about one hour on it - is basically necessary if you want to write an ansible script.)
* Start using terminal and practice navigating the unix filesystem on your own.

### Unix Cheat Sheet
Find out where you are with `pwd`:
```
Simfarm@chrwang-OSX:~$ pwd
/Users/Simfarm
```

Find out out the files in your directory with `ls`:
```
Simfarm@chrwang-OSX:~$ ls
Applications/    Documents/       Dropbox/         Library/         Music/           Pictures/        VirtualBox VMs/
Desktop/         Downloads/       Git/             Movies/          OpenShift/       Public/          __pycache__/
```

Move file with `mv`:
```
Simfarm@chrwang-OSX:~$ mv inventory /root/inventory
```
* Arguments are as follows: first comes target file and the second is target file destination.

Navigate somewhere else with `cd`.
* Navigate one level "down":
```
Simfarm@chrwang-OSX:~/Documents$ pwd
/Users/Simfarm/Documents
Simfarm@chrwang-OSX:~/Documents$ cd ..
Simfarm@chrwang-OSX:~$ pwd
/Users/Simfarm
```
* Navigate one level "up":
```
Simfarm@chrwang-OSX:~$ pwd
/Users/Simfarm
Simfarm@chrwang-OSX:~$ cd Documents/
Simfarm@chrwang-OSX:~/Documents$ pwd
/Users/Simfarm/Documents
```
