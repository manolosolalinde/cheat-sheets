# Useful Linux commands

Sort package list by size
```bash
dpkg-query -W --showformat='${Installed-Size;10}\t${Package}\n' | sort -k1,1n
```
List file and folder sizes in a directory
```bash
du -sh *
```
Know the free space in a disk
```bash
df -h .
```

# Useful random commands
`lsof -i `
`export FLASK_APP=application.py`
Check conection to host
`telnet localhost 7000`


