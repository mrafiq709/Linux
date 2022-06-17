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
