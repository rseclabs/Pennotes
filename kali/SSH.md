# SSH
Set an ssh tunnel.  For example, tunnel VNC.
```
ssh -N -X -Y -C -g -L 5901:localhost:5901 root@<remote host> &
```
ssh to server with older ciphers
```
ssh -oKexAlgorithms=<ciphers offered> <usernae>@<IP>
```
