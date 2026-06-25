# Day 02: Create Temporary User Account with Defined Expiry Date

## 📌 Task Objective

Configure a time-limited system user account on an application server with an explicit expiration date to enforce strict, temporary access controls for external or short-term contractors.

## 🗺️ System Scope & Logic

| Target Node | Target Username | Expiry Date | Target Utility | Primary Verification Utility |
| --- | --- | --- | --- | --- |
| App Server 1 | `jim` | `2024-02-17` | `useradd` | `chage` |

## 🛠️ Implementation & Commands

```bash
# Create the user with an expiry date
sudo useradd -e 2024-02-17 jim

```

## 🔍 Verification & Testing

```bash
# Verify account expiry details
sudo chage -l jim

# Confirm user creation
getent passwd jim

```

* Expected output from `chage` explicitly details "Account expires : Feb 17, 2024".
* Expected entry returned from `getent passwd` verifies the user exists on the local system template.

## 🛑 Troubleshooting & Roadblocks

Initial configuration successful; no blockers encountered.

## 💡 Key Architectural Takeaways

* **Operational Insight:** Leveraging metadata flags within the system shadow files instructs the Pluggable Authentication Modules (PAM) architecture to block access automatically at midnight UTC on the specified date without needing manual administrative intervention.
* **Production Context:** Enforcing strict account lifecycle policies prevents stale user credentials from lingering indefinitely on critical workloads, drastically shrinking the potential attack surface of enterprise infrastructure.