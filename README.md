# Linux

Cache Details
---------------
`wmic cpu get L2CacheSize, L3CacheSize`

ssh download file
------------------
with ssh key
```
scp hostname:/remote/dir/foobar.txt /local/dir
```
with .pem file
```
scp -i key_file.pem your_username@remotehost.edu:/remote/dir/foobar.txt /local/dir
```
Change php version:
-------------------
```
sudo update-alternatives --config php
```
https://help.clouding.io/hc/en-us/articles/360021630059-How-to-Install-Multiple-PHP-Versions-7-2-7-4-and-8-0-on-Ubuntu-20-04

Sending email permission denied from server (SELINUX Issue)
---------------------
First try disabling SELINUX to see if it is SELINUX issue or not
```
sudo setenforce 0
```
Now send email, if it is success then SELINUX is blocking your email
Now enable it again and try generate same error again
```
sudo setenforce 1
```
Check SELINUX log
```
sudo ausearch -m avc -ts recent
```
It will output something like this for the recent blocked email or port
```
time->Sat Aug 31 12:08:44 2024
type=PROCTITLE msg=audit(1725106124.349:13953853): proctitle=2F7573722F7362696E2F6874747064002D44464F524547524F554E44
type=SYSCALL msg=audit(1725106124.349:13953853): arch=c000003e syscall=42 success=no exit=-13 a0=11 a1=7f404fe72550 a2=10 a3=66d307cc items=0 ppid=9343 pid=6555 auid=4294967295 uid=48 gid=48 euid=48 suid=48 fsuid=48 egid=48 sgid=48 fsgid=48 tty=(none) ses=4294967295 comm="httpd" exe="/usr/sbin/httpd" subj=system_u:system_r:httpd_t:s0 key=(null)
type=AVC msg=audit(1725106124.349:13953853): avc:  denied  { name_connect } for  pid=6555 comm="httpd" dest=465 scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:smtp_port_t:s0 tclass=tcp_socket permissive=0
----
time->Sat Aug 31 12:08:44 2024
type=PROCTITLE msg=audit(1725106124.349:13953854): proctitle=2F7573722F7362696E2F6874747064002D44464F524547524F554E44
type=SYSCALL msg=audit(1725106124.349:13953854): arch=c000003e syscall=42 success=no exit=-13 a0=11 a1=7f404feaee00 a2=1c a3=66d307cc items=0 ppid=9343 pid=6555 auid=4294967295 uid=48 gid=48 euid=48 suid=48 fsuid=48 egid=48 sgid=48 fsgid=48 tty=(none) ses=4294967295 comm="httpd" exe="/usr/sbin/httpd" subj=system_u:system_r:httpd_t:s0 key=(null)
type=AVC msg=audit(1725106124.349:13953854): avc:  denied  { name_connect } for  pid=6555 comm="httpd" dest=465 scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:smtp_port_t:s0 tclass=tcp_socket permissive=0
```
Now I see from here SELINUX is blocking **comm=httpd** is with **dest=465** 
So create new rules to allow it
```
sudo setsebool -P httpd_can_sendmail 1
```
Now verify changes
```
sudo getsebool httpd_can_sendmail
```
Done !!!
