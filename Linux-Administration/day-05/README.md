# Day 05: Disable SELinux Configuration

## 📌 Task Objective

Install essential SELinux administration packages and permanently disable the SELinux security framework within the system configuration on App Server 2 without triggering a node reboot.

## 🗺️ System Scope & Logic

| Target Node | Target Configuration File | Parameter Modified | Target State |
| --- | --- | --- | --- |
| App Server 2 | `/etc/selinux/config` | `SELINUX` | `disabled` |

## 🛠️ Implementation & Commands

```bash
# Install SELinux packages
yum install -y selinux-policy selinux-policy-targeted libselinux-utils policycoreutils

# Disable SELinux permanently in config
sed -i 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config


```

## 🔍 Verification & Testing

Validate the persistent configuration modifications by querying the SELinux configuration file to ensure the directive is explicitly set to disabled.

```bash
# Verify SELinux config change
grep "^SELINUX=" /etc/selinux/config
# Expected Output: SELINUX=disabled

```

## 🛑 Troubleshooting & Roadblocks

Initial configuration successful; no blockers encountered.

## 💡 Key Architectural Takeaways

* **Operational Insight:** The persistent operational state of SELinux is governed entirely by the `/etc/selinux/config` configuration file, which reads policies at early boot stages rather than tracking dynamic runtime overrides.
* **Production Context:** Disabling SELinux is often required in legacy production enterprise environments to prevent complex permission blocks on custom, non-standard application ports and file paths when custom policies have not yet been authored.