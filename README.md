# 📂 Ansible Collections: System Namespace

A centralized repository for managing Ansible collections related to system configuration and management.

---

#### 📚 Collections Included

- ✅ `ansible.posix`
- ✅ `community.general`
- ✅ `ansible.utils`
- ✅ `ansible.builtin`

---

#### 🗂️ Folder Structure

```
System/
│
├── playbooks/
│   ├── install.yml
│   ├── configure.yml
│   └── security.yml
│
├── roles/
│   ├── common/
│   ├── users/
│   └── network/
│
├── inventory/
│   ├── hosts.ini
│   └── group_vars/
│
└── collections/
```

---

#### 🛠️ Usage

1. Install the required collections:

`````
```bash
ansible-galaxy collection install -r requirements.yml
```
`````

2. Run the playbook:

`````
```bash
ansible-playbook -i inventory/hosts.ini playbooks/install.yml
```
`````

---

#### ⚡ Requirements

- Ansible 2.9+
- Supported Linux distribution

---

#### 📄 License

MIT

---

#### 👤 Author

Rajarshi GANGULY

