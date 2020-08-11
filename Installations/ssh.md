# ssh

ssh (Secure Shell).

We can use ssh to remotely login servers and execute commands. 
So we can sit at home and ask the server at campus to run our codes.  

## How to ssh ccgo (or other hosts)?

### Step 1: [vpn to campus](https://wikis.utexas.edu/display/BMEIT/Access+UT%27s+VPN)

### Step 2: ssh to the host.

[Tutorial](https://www.oden.utexas.edu/sysdocs/ssh/index.html) on sysnet.

First you need to have Oden Institute usename. For example, mine is mathewhu.
Then you need to know the host name you want to ssh. For example, ccgo host names are ccgo1 and ccgo2 (@oden.utexas.edu).

Just run following command in the terminal.
```
ssh <username>@<hostname>
```
For example, to ssh ccgo1 with my username mathewhu.
```
ssh mathewhu@ccgo1.oden.utexas.edu
```
When connecting to a server at the first time, it will ask you to confirm the server. 
Once you confirm it, your computer will remember it and won't ask you again.
Then it will ask for your password, which is the Oden Institute password. 
Enter it and you are in. 

## Tips
### 1. passwordless login
Run this command in the terminal, 
```
ssh-keygen
```
and follow the instruction (or you can just keep pressing enter). This will generate you rsa key. 
Then, with vpn connecting to the campus, use following command to send your public key to the host.
```
ssh-copy-id -i ~/.ssh/id_rsa <user>@<host>.oden.utexas.edu
```
You are all set. Now you can ssh to this server without password.

### 2. ssh config
We can set the username and hostname in advance, in order to ssh with a short command. 
Generate a file from home directory 
```
.ssh/config
```
and add (for example, to ssh ccgo1 with user name mathewhu)
```
Host ccgo1
        Hostname ccgo1.oden.utexas.edu
        User mathewhu
```
Now I can get access by only 
```
ssh ccgo1
```

### 3. ssh without vpn
use Proxy Jump:
```
ssh -J mathewhu@login1.oden.utexas.edu mathewhu@ccgo1.oden.utexas.edu
```
Or, in the config file, add
```
Host login1
        Hostname login1.oden.utexas.edu
        User mathewhu
Host ccgo1
        Hostname ccgo1.oden.utexas.edu
        User mathewhu
        ProxyJump login1
```
