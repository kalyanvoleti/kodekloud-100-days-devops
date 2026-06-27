# Day 07: Configure Password-less SSH Authentication

## 📌 Task Objective

Establish secure, password-less SSH authentication from the central jump host to all corporate application servers to facilitate automated, non-interactive remote management.

## 🗺️ System Scope & Logic

| Target Node | Host IP | Sudo Username | Authentication Type |
| --- | --- | --- | --- |
| Jump Host | Localhost | thor | Public/Private Key Pair |
| App Server 1 | 172.16.238.10 | tony | Authorized Keys |
| App Server 2 | 172.16.238.11 | steve | Authorized Keys |
| App Server 3 | 172.16.238.12 | banner | Authorized Keys |

## 🛠️ Implementation & Commands

```bash
# Generate a high-entropy RSA key pair on the jump host
ssh-keygen -t rsa -b 4096

# Distribute the public key to the target application servers
ssh-copy-id tony@172.16.238.10
ssh-copy-id steve@172.16.238.11
ssh-copy-id banner@172.16.238.12


```

## 🔍 Verification & Testing

Validate non-interactive access by establishing an SSH session to each application server, ensuring access is granted immediately without a password prompt.

```bash
ssh tony@172.16.238.10
ssh steve@172.16.238.11
ssh banner@172.16.238.12

```

## 🛑 Troubleshooting & Roadblocks

Initial configuration successful; no blockers encountered.

## 💡 Key Architectural Takeaways

* **Operational Insight:** The `ssh-copy-id` utility automates the placement of a client's public key into the remote target user's `~/.ssh/authorized_keys` file while ensuring the correct restrictive file permissions are enforced.
* **Production Context:** Password-less public key authentication is a fundamental prerequisite for configuration management systems, CI/CD runners, and orchestration tools to execute automated deployments across multi-node infrastructure without manual intervention.