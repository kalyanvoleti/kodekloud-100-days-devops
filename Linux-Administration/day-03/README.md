# Day 03: Disable Direct SSH Root Login

## 📌 Task Objective

Enhance the overall security posture across the Stratos Datacenter infrastructure by disabling direct SSH root access on all application servers. This requirement enforces administrative accountability and mitigates unauthorized brute-force attack vectors targeting the privileged root account.

## 🗺️ System Scope & Logic

| Target Node | Usernames | Directories | Permissions / Configurations |
| --- | --- | --- | --- |
| App Server 1 (`172.16.238.10`) | root | `/etc/ssh` | `PermitRootLogin no` |
| App Server 2 (`172.16.238.11`) | root | `/etc/ssh` | `PermitRootLogin no` |
| App Server 3 | root | `/etc/ssh` | `PermitRootLogin no` |

## 🛠️ Implementation & Commands

```bash
# App Server 1
sudo vi /etc/ssh/sshd_config
sudo systemctl restart sshd

# App Server 2
sudo vi /etc/ssh/sshd_config
sudo systemctl restart sshd

# App Server 3
sudo vi /etc/ssh/sshd_config
sudo systemctl restart sshd

```

## 🔍 Verification & Testing

Verify that remote daemon authentication restrictions have been successfully applied by executing a direct root login attempt against the managed server nodes. Access must be explicitly denied by the service.

```bash
ssh root@172.16.238.10
ssh root@172.16.238.11

```

## 🛑 Troubleshooting & Roadblocks

Initial configuration successful; no blockers encountered.

## 💡 Key Architectural Takeaways

* **Operational Insight:** Modifying core directives within `/etc/ssh/sshd_config` alters the static configuration state, requiring an explicit service restart (`systemctl restart sshd`) to flush the runtime configuration and commit adjustments to active memory.
* **Production Context:** Disabling direct root login paths enforces mandatory non-repudiation in production clouds. Administrative access must originate from a dedicated user session before escalating permissions via `sudo`, establishing a transparent, auditable trail of ownership.