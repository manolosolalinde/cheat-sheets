# Postgresql Startup guide

Installation UBUNTU\
`sudo apt-get install postgresql`

You can now start the database server using:\
`sudo /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/main -l logfile start`

Add Environment variables to /etc/bash.bashrc
```bash
PATH=/usr/lib/postgresql/10/bin:$PATH
export PATH

LD_LIBRARY_PATH=/usr/lib/postgresql/10/lib
export LD_LIBRARY_PATH

MANPATH=/usr/lib/postgresql/10/share/man:$MANPATH
export MANPATH
```
Initialize database cluster
```bash
source /etc/bash.bashrc
sudo ldconfig
mkdir /usr/local/pgsql
sudo passwd postgres
sudo chown postgres /usr/local/pgsql
su postgres
initdb -D /usr/local/pgsql/data
```
Start database server
```bash
cd /usr/local/pgsql/data/
pg_ctl -D /usr/local/pgsql/data -l logfile start
```
Stop the server
```bash
kill -INT `head -1 /usr/local/pgsql/data/postmaster.pid`
```
Check if server is running
```bash
lsof -i
```

# Create a database
```bash
psql
```
```sql
CREATE DATABASE mydatabase;
```

# Run script
export DATABASE_URL="postgres://postgres:pass@localhost:5432/mydatabase"
psql -d $DATABASE_URL -a -f script.sql
psql -d postgres://postgres:pass@localhost:5432/mydatabase -a -f script.sql