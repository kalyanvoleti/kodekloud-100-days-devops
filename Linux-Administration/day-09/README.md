# Day 09: Recover MariaDB Service

## 📌 Task Objective

Investigate and restore a failed MariaDB database instance on the Nautilus database server by resolving critical underlying filesystem and runtime directory permission errors.

## 🗺️ System Scope & Logic

| Target Node | Target Service | Affected Directories | Correct Ownership |
| --- | --- | --- | --- |
| Nautilus Database Server | MariaDB | `/var/lib/mysql`, `/run/mariadb` | `mysql:mysql` |

## 🛠️ Implementation & Commands

```bash
sudo systemctl status mariadb
sudo chown -R mysql:mysql /var/lib/mysql
sudo systemctl start mariadb
ls -ld /run/mariadb
sudo chown -R mysql:mysql /run/mariadb
sudo systemctl start mariadb
sudo systemctl status mariadb

```

## 🔍 Verification & Testing

Executed `sudo systemctl status mariadb` to validate the operational health of the database engine, confirming that the service successfully transitioned into an `Active: active (running)` state.

## 🛑 Troubleshooting & Roadblocks

* **Issue:** The MariaDB service failed to initialize during startup due to incorrect directory ownership on the `/run/mariadb` runtime path, blocking the process from writing its PID and socket files.
* **Resolution:** Corrected the ownership configuration by executing `sudo chown -R mysql:mysql /run/mariadb`, which immediately allowed the systemd service unit to start successfully.

## 💡 Key Architectural Takeaways

* **Operational Insight:** Systemd service units often depend on transient runtime directories (like `/run/`) that require specific user and group ownership permissions to create sockets and pidfiles during initialization.
* **Production Context:** Enforcing exact ownership and permissions across data and runtime paths prevents service degradation and ensures high availability for critical application data stores.