# PostgreSQL administration

[← back](../linux-sql.md)

## 1. PostgreSQL server commands

On most modern Linux distributions, the PostgreSQL server is managed with `systemd`.

```bash
# start
sudo systemctl start postgresql

# stop
sudo systemctl stop postgresql

# restart
sudo systemctl restart postgresql

# enable at boot
sudo systemctl enable postgresql

# enable at boot and start immediately
sudo systemctl enable --now postgresql

# disable at boot
sudo systemctl disable postgresql

# disable at boot and stop immediately
sudo systemctl disable --now postgresql
```

Check the server status:

```bash
sudo systemctl status postgresql
```

If the system uses a version-specific unit, the service name may be different, for example:

```bash
sudo systemctl restart postgresql@16-main
```
