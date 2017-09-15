## Setting up the VM with ssh ability

  1. Need to install openssh-server

```
sudo rm /etc/ssh/ssh_config
sudo apt-get purge openssh-server
sudo apt-get install openssh-server
```

  2. Set up the network and shared folder
    - NAT
    - Add port with something like `{ hostPort: 22, guestPort: 2222 }`
    - for shared folder, select `auto-mount` and `make permanent`

  3. Restart the VM

  4. ssh into the VM
    - `TERM=xterm ssh -Xp 2222 cs6430@localhost` (actually type `localhost`)

  5. Add your user to the vbox group for shared folders
    - `sudo adduser cs6340 vboxsf`

  6. Log out and back in to VM

  7. Change user permissions of shared folder
    - `chmod -R 777 /media/<your shared folder name>/`
