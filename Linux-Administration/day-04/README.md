# Day 04: Grant Execute Permissions to Backup Script

## 📌 Task Objective

Configure filesystem permissions on a target application host to allow global execution of a critical system backup script. This ensures automated and unprivileged local users can run the task without elevating to root privileges.

## 🗺️ System Scope & Logic

| Target Node | Target File Path | Current Owner/Group | Target Permissions (Octal) | Scope of Execution |
| --- | --- | --- | --- | --- |
| App Server 3 | `/tmp/xfusioncorp.sh` | `root` / `root` | `755` (`-rwxr-xr-x`) | All local system users |

## 🛠️ Implementation & Commands

```bash
# Checked existing permissions
ls -l /tmp/xfusioncorp.sh

# Updated permissions to allow execution
sudo chmod 755 /tmp/xfusioncorp.sh

# Verified permissions after change
ls -l /tmp/xfusioncorp.sh

# Tested script execution without sudo
sh /tmp/xfusioncorp.sh
./tmp/xfusioncorp.sh
bash /tmp/xfusioncorp.sh

```

## 🔍 Verification & Testing

Executed explicit file status checks and non-root execution tests to confirm configuration validity:

* Ran `ls -l /tmp/xfusioncorp.sh` to confirm the mode bits updated successfully to `-rwxr-xr-x`.
* Executed `./tmp/xfusioncorp.sh` directly as an unprivileged user, resulting in a successful run and printing the valid output payload: `Welcome To KodeKloud`.

## 🛑 Troubleshooting & Roadblocks

Initial configuration successful; no blockers encountered.

## 💡 Key Architectural Takeaways

* **Operational Insight:** Direct binary or script execution via standard shell invocation (`./script.sh`) requires explicit execute mode bits (`+x`) set on the file descriptor, whereas passing the file directly as an argument to an interpreter (e.g., `bash script.sh`) only requires read permissions.
* **Production Context:** Utilizing explicit octal permissions like `755` ensures scripts are globally readable and executable by automated automation agents or system peers while strictly confining write access to the administrative owner, enforcing the principle of least privilege.