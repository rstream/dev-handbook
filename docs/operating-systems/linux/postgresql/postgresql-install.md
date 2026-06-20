# PostgreSQL installation and setup

[← back](../dev/linux-sql.md)

## Installation

Install PostgreSQL on Linux (client and server)
```sh
sudo zypper install postgresql postgresql-server
```

If you are planning to use PostgreSQL with PHP, also install
```sh
sudo zypper install php8-pgsql
```

Enable PostgreSQL service at boot (and start now)
```sh
sudo systemctl enable --now postgresql
```

## pgAdmin

### Install pgAdmin (desktop version)

Install pgAdmin (desktop version)
```sh
sudo zypper install pgadmin4-desktop
```

### Set up password for `postgres` user

Enter psql shell as `postgres` user
```shell
su -
runuser -u postgres -- psql
```
Set the password for `postgres` user
```sh
ALTER USER postgres WITH PASSWORD '0000';
exit
```
Set up authorizations for `postgres` user
```sh
sudo nano /var/lib/pgsql/data/pg_hba.conf
```
Replace this:
```
local   all   all                  peer
host    all   all   127.0.0.1/32   ident
host    all   all   ::1/128        ident
```

to this:
```
local   all   all                  scram-sha-256
host    all   all   127.0.0.1/32   scram-sha-256
host    all   all   ::1/128        scram-sha-256
```
