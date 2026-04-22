# SQL for Linux

[← back](index.md)

## PostgreSQL

### 1. Installation

Install PostgreSQL on Linux (  
```sh
sudo zypper install postgresql postgresql-server
```

### 2. Enable service

To make the PostgreSQL server run on startup
```sh
sudo systemctl enable postgresql
```
Note: this will not start the service right now.

### 3. Start service
```sh
sudo systemctl start postgresql
```
