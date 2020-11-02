```
# SERVER FROM HELL WRITEUP
#### Author: DeadPackets
[Task 1] Flag.txt | "Start at port 1337 and enumerate your way."\n
First connect to port 1337 with nc,
output:

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
NFS shares are cool, especially when they are misconfigured
It's on the standard port, no need for another scan













