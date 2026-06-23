# Day 01: Create Custom User with Explicit UID and Home Directory

## 📌 Task Objective

Configure a dedicated system user account with an explicitly assigned unique identifier (UID) and a custom home path on an application server to isolate a web service process.

## 🗺️ System Scope & Logic

| Target Node | Target Username | Assigned UID | Home Directory | Default Shell |
| --- | --- | --- | --- | --- |
| App Server 1 (`172.16.238.10`) | `kareem` | `1265` | `/var/www/kareem` | `/bin/bash` |

## 🛠️ Implementation & Commands

```bash
# Connect to App Server 1
ssh tony@172.16.238.10

# Create the home directory
sudo mkdir -p /var/www/kareem

# Create user with specific UID and custom home directory
sudo useradd -u 1265 -d /var/www/kareem -s /bin/bash kareem

# Assign ownership of the home directory to the user
sudo chown -R kareem:kareem /var/www/kareem

```

## 🔍 Verification & Testing

```bash
# Verify user and directory properties
id kareem
ls -ld /var/www/kareem

```

* Expected output confirms the user `kareem` matches UID `1265`.
* Expected directory listings confirm `/var/www/kareem` is owned exclusively by `kareem:kareem`.

## 🛑 Troubleshooting & Roadblocks

Initial configuration successful; no blockers encountered.

## 💡 Key Architectural Takeaways

* **Operational Insight:** Decoupling a service account from standard default properties prevents ID collisions and stops systems from populating user files into standard global fallback paths like `/home`.
* **Production Context:** Hardening Linux instances requires isolating web platform processes within strict, non-default paths with custom execution restrictions to contain the blast radius if an application exploit occurs.