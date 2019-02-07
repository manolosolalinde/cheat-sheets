# Useful Linux commands

Sort package list by size
```bash
dpkg-query -W --showformat='${Installed-Size;10}\t${Package}\n' | sort -k1,1n
```
Find all python installations
```bash
for p in $(compgen -c python); do printf "%-16s" $p; $p --version; done
```

List file and folder sizes in a directory
```bash
du -sh *
```
Know the free space in a disk
```bash
df -h .
```
Open file explorer in folder
```bash
xdg-open file_or_dir
```

# Linux environment variables

List environment variables
```bash
printenv
```

Export environment variable
```bash
export FLASK_APP=application.py
```

Show one variables
```bash
echo $PATH
```

Set global environment variables for system: ```/etc/environment```

Set global environment variables for my session: ```~/.bashrc``` add lines ```export VAR=xxx```

# Useful random commands

List open connections\
`lsof -i `



Check conection to host\
`telnet localhost 7000`

Set ubuntu for no password

    First, if your user has sudo privileges, you must enable its NOPASSWD option. Otherwise, sudo will ask for a password even when you don't have one, and won't accept an empty password. To do so, open the sudoers configuration file with sudo visudo, and add the following line to the file, replacing manolosolalinde with your username:
    manolosolalinde ALL=(ALL) NOPASSWD:ALL
    Close the editor to apply the changes, and test the effect on sudo in a new terminal.
    Delete the password for your user by running this command:
    sudo passwd -d `whoami`