adding swapfile
```
fallocate -l 1G /swapfile # creates a swap file
chmod 600 /swapfile # preventing regular users from reading it
mkswap /swapfile # sets up the Linux swap area
swapon /swapfile # enables the file for swapping
```