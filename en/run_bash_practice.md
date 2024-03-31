---
lang: en
layout: home
lang-ref: run_bash_practice
---

## Run Bash. Debugging

Here a list of possible files which are used when a shell is started:

```bash
/etc/profile
~/.bash_profile
~/.bash_login
~/.profile

/etc/bash.bashrc
~/.bashrc
```

and when it exits:

```bash
/etc/bash.bash.logout
~/.bash_logout
```

Experiments will be done in a container with Debian:

```bash
docker run -it debian /bin/bash
```

Create above-mentioned files and add there debugging information:

```
root@a2fb609d1edf:/# echo 'echo "/etc/profile" >> /tmp/bash.log' >> /etc/profile
root@a2fb609d1edf:/# echo 'echo "~/.bash_profile" >> /tmp/bash.log' >> ~/.bash_profile
root@a2fb609d1edf:/# echo 'echo "~/.bash_login" >> /tmp/bash.log' >> ~/.bash_login
root@a2fb609d1edf:/# echo 'echo "~/.profile" >> /tmp/bash.log' >> ~/.profile
root@a2fb609d1edf:/# echo 'echo "/etc/bash.bashrc" >> /tmp/bash.log' >> /etc/bash.bashrc
root@a2fb609d1edf:/# echo 'echo "~/.bashrc" >> /tmp/bash.log' >> ~/.bashrc
root@a2fb609d1edf:/# echo 'echo "/etc/bash.bash.logout" >> /tmp/bash.log' >> /etc/bash.bash.logout
root@a2fb609d1edf:/# echo 'echo "~/.bash.logout" >> /tmp/bash.log' >> ~/.bash.logout
```

#### Launch it

```bash
root@a2fb609d1edf:/# bash
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
~/.bashrc

root@a2fb609d1edf:/# bash -i
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
~/.bashrc

root@a2fb609d1edf:/# bash -s hello
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
~/.bashrc

root@a2fb609d1edf:/# bash -c 'ls'
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin srv  sys  tmp  usr  var
root@a2fb609d1edf:/# ls /tmp/bash.log
ls: cannot access '/tmp/bash.log': No such file or directory

root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
/etc/profile
~/.bash_profile

root@a2fb609d1edf:/# bash -r
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
~/.bashrc

root@a2fb609d1edf:/# bash --noprofile
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
~/.bashrc

root@a2fb609d1edf:/# bash --noprofile -l
bash-5.0# cat /tmp/bash.log
cat: /tmp/bash.log: No such file or directory

root@a2fb609d1edf:/# bash --norc
bash-5.0# cat /tmp/bash.log
cat: /tmp/bash.log: No such file or directory

root@a2fb609d1edf:/# bash --posix
bash-5.0# cat /tmp/bash.log
cat: /tmp/bash.log: No such file or directory

root@a2fb609d1edf:/# bash -i -l  
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
/etc/profile
~/.bash_profile

root@a2fb609d1edf:/# bash -r -i 
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
~/.bashrc

root@a2fb609d1edf:/# bash -r -l
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
/etc/profile
~/.bash_profile

root@a2fb609d1edf:/# bash -r -l -i
root@a2fb609d1edf:/# cat /tmp/bash.log
/etc/bash.bashrc
/etc/profile
~/.bash_profile
```
