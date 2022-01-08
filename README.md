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
