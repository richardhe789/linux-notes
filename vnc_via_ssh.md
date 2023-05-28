# To VNC to another computer over SSH securely

```
1. Windows machine AA  
|  
|  
2. Linux machine BB  
|  
|  
----------------------------  
3. Insecure public Internet  
----------------------------  
|  
|  
4. Linux machine CC  
|  
|  
5. Solaris machine DD running VNCserver on display :01
```
  
To access the solaris machine DD from the windowns machine AA.

run this command on Linux machine BB.  
```
ssh -g -L 5933:HOST_NAME_DD:5901 HOST_IP_CC  
```
After you can login, run this on Windows machine AA  
```
vncviewer HOST_IP_BB:33
```
enter your VNC password as you defined on Solaris machine DD,  
you are running VNC over SSH securely

 ``` 
-L listen-port:host:port Forward local port to remote address  
-g Allow remote hosts to connect to forwarded ports.
```
