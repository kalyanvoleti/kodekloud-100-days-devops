# Day 08: Install Ansible via Pip3

## 📌 Task Objective

Deploy a specific version of Ansible globally on the jump host utilizing the Python package manager to ensure configuration management tools are accessible across all user profiles.

## 🗺️ System Scope & Logic

| Target Node | Usernames | Installation Method | Target Package & Version |
| --- | --- | --- | --- |
| Jump Host | `standard_user` / `root` | `pip3` (Global via `sudo`) | `ansible==4.10.0` |

## 🛠️ Implementation & Commands

```bash
# Check pip3 availability and version
pip3 --version

# Install specific Ansible version globally
sudo pip3 install ansible==4.10.0

```

## 🔍 Verification & Testing

Execute package inspections and binary version checks across both standard and superuser environments to validate global availability:

```bash
# Verify installation details and command availability as local user
pip3 show ansible
ansible --version

# Switch to root environment to validate global path availability
sudo su -
pip3 show ansible
ansible --version

```

## 🛑 Troubleshooting & Roadblocks

Initial configuration successful; no blockers encountered.

## 💡 Key Architectural Takeaways

* **Operational Insight:** Installing packages via `sudo pip3` places executables into shared system binary paths (typically `/usr/local/bin`), rendering the application accessible globally across distinct user shell profiles rather than isolating it to a single user's `~/.local` path.
* **Production Context:** Utilizing explicit version pinning (`ansible==4.10.0`) within automation bootstrap scripts guarantees environment consistency across immutable infrastructure and prevents deployment failures caused by untracked upstream updates.