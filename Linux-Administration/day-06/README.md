# Day 06: Automate Cron Job Deployment via Ansible

## 📌 Task Objective

Automate the installation of the cron daemon and schedule a recurring system validation task across all distributed application nodes using centralized configuration management.

## 🗺️ System Scope & Logic

| Target Node | System Users | Target Directories | Playbook Configurations |
| --- | --- | --- | --- |
| Nautilus App Servers | `root` / Ansible Remote User | `~/cron-test`, `/tmp` | Package: `cronie`, Output: `/tmp/cron_text` |

## 🛠️ Implementation & Commands

```bash
sudo su -
mkdir ~/cron-test && cd ~/cron-test
ansible-playbook playbook.yml

```

## 🔍 Verification & Testing

Validate that the cron configuration applied correctly and executed successfully by verifying the generation and content of the destination output file across all target inventory hosts using the Ansible ad-hoc shell module:

```bash
ansible all -m shell -a "cat /tmp/cron_text"

```

## 🛑 Troubleshooting & Roadblocks

* **Issue:** SSH authentication blocked due to host key trust verification during execution.
* **Resolution:** Configured trusted host key handling or disabled rigid host key checking within the Ansible environment parameters.


* **Issue:** Remote sudo privilege escalation failed during playbook runtime execution.
* **Resolution:** Defined explicit password-based privilege escalation variables by appending `ansible_become_pass` within the centralized host inventory.



## 💡 Key Architectural Takeaways

* **Operational Insight:** The underlying `cronie` package management workflow requires explicit service state validation and initialization following package deployment to ensure the background scheduling daemon actively processes new crontab definitions.
* **Production Context:** Utilizing declarative automation to manage background system schedules eliminates manual scheduling drift across large-scale infrastructure fleets, maintaining consistent administrative and maintenance states across all target compute layers.