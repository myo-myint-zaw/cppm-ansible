# ClearPass Automation with Ansible

This project automates Aruba ClearPass configuration using Ansible and Jinja2 templates. It reads provisioning data from an Excel file and pushes configurations via API.

---

## 📁 Directory Structure

```
clearpass-automation/
├── playbooks/
│   └── apply_clearpass_config.yml
├── roles/
│   └── clearpass/
│       ├── tasks/
│       │   ├── main.yml
│       │   ├── apply_access_devices.yml
│       │   ├── apply_device_groups.yml
│       │   ├── apply_enforcement_policy.yml
│       │   ├── apply_role.yml
│       │   ├── apply_role_mapping.yml
│       ├── templates/
│       │   ├── access_device.json.j2
│       │   ├── device_group.json.j2
│       │   ├── enforcement_policy.json.j2
│       │   ├── role.json.j2
│       │   ├── role_mapping.json.j2
│       └── vars/
│           └── main.yml
├── inventory/
│   ├── hosts.yml
│   ├── group_vars/
│   │   └── clearpass.yml
│   └── host_vars/
├── files/
│   └── combined_clearpass_data.xlsx
```

---

## ⚙️ Configuration

Edit `inventory/group_vars/clearpass.yml`:

```yaml
client_id: cppm_client_credential
client_secret: your_clearpass_secret
sheet_name: Enforcement_Policy
rows_to_execute: "1-50"
```

---

## 🧾 Supported Excel Sheets

Each sheet maps to a task and Jinja2 template:

| Sheet Name          | Description                        |
|---------------------|------------------------------------|
| Access_Devices       | Adds Network Devices               |
| Device_Groups        | Creates Device Groups              |
| Role                 | Defines Role Objects               |
| Role_Mapping         | Maps AD groups to Roles            |
| Enforcement_Policy   | Creates TACACS Enforcement Policies|

**Sample Columns (for Enforcement_Policy):**

| name | description | default_enforcement_profile | enforcement_profile_names | role_name |

---

## 🚀 Usage

1. Place your Excel file in the `files/` directory.
2. Adjust variables in `group_vars/clearpass.yml`.
3. Run the playbook:

```bash
ansible-playbook -i inventory/hosts.yml playbooks/apply_clearpass_config.yml
```

---

## 📝 Notes

- Requires `community.general` collection for Excel support.
- SSL validation is disabled (`validate_certs: false`) for testing. Change this in production.
- Ensure ClearPass API is accessible and credentials are correct.

---

## 🔧 Install Required Collection

```bash
ansible-galaxy collection install community.general
```
## 📫 Author

**Myo Myint Zaw**  
Feel free to reach out or fork the repo for enhancements!
