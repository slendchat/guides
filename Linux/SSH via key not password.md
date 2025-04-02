
### SSH from windows to LINUX


### SSH from linux to *

First generate key on Linux machine with 

Command:
```
ssh-keygen -t rsa
```

Explanation of command:
- `ssh-keygen`: the tool to create SSH keys.
- `-t rsa`: specifies the **type** of key to generate — in this case, RSA

The example output (i used no password for this key):
```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/art/.ssh/id_rsa):
/home/art/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/art/.ssh/id_rsa
Your public key has been saved in /home/art/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:fNEzCPMBGL/e2JzFiy29Qou86J4m1obWLWcaX2fix6M art@vm1usm
The key's randomart image is:
+---[RSA 3072]----+
|      .o+..      |
|      .. + +     |
|        . + +    |
|       . . o o   |
|        S . o    |
|       . *.* .   |
|     +.oooXo*    |
|    = *=*oo=+.   |
|   o **=o.E+..   |
+----[SHA256]-----+
```

Copy your public key to an existing server, make sure you know password of account you are copying key.

Command 
```
ssh-copy-id art@192.168.109.143
```

To use the utility, you need to specify the remote host that you would like to connect to, and the user account that you have password-based SSH access to. This is the account where your public SSH key will be copied.

then just ssh art@192.168.109.143, and it goes.