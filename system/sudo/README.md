# 🛡️ Ansible Playbook: Sudo Installation and Configuration

A minimal Ansible playbook to manage `sudo` installation, user creation, and permission configuration.

---

#### ✨ Features

- 🛠️ Install `sudo`
- 👤 Create a system group and user
- 🔑 Add the user to the `sudo` group
- 📂 Configure the `.ssh` directory and `authorized_keys` file
- 🛡️ Grant passwordless `sudo` privileges

---

#### 📋 Playbook Structure

`````
### 📦 Install the `sudo` Package
```yaml
- name: Installer les packet requis
  ansible.builtin.apt:
    name: sudo
    state: present
```

### 🛡️ Create the Group
```yaml
- name: Adding the group {{ sudo_user }}
  ansible.builtin.group:
    name: "{{ sudo_user }}"
    state: present
    system: true
```

### 👤 Create the User
```yaml
- name: Making the user {{ sudo_user }}
  ansible.builtin.user:
    name: "{{ sudo_user }}"
    append: true
    createhome: true
    system: true
    groups: "{{ sudo_user }}"
    state: present
    shell: /bin/bash
```

### ➕ Add User to Sudo Group
```yaml
- name: Adding the {{ sudo_user }}
  ansible.builtin.shell: |
    adduser "{{ sudo_user }}" sudo
    usermod -a -G sudo "{{ sudo_user }}"
```

### 🔒 Configure Authorized Keys
```yaml
- name: Creation du la ficher authrorized_keys si ca nest existe pas
  ansible.builtin.file:
    path: "{{ item.path }}"
    owner: "{{ sudo_user }}"
    group: "{{ sudo_user }}"
    state: "{{ item.state }}"
    mode: "{{ item.mode }}"
  loop:
    - {path: "/home/{{ sudo_user }}/.ssh", state: directory, mode: 700}
    - {path: "/home/{{ sudo_user }}/.ssh/authorized_keys", state: touch, mode: 600}
```

### ✅ Grant Sudo Privileges
```yaml
- name: Adding in the sudo file ---> {{ sudo_user }}
  ansible.builtin.lineinfile:
    path: /etc/sudoers
    state: present
    regexp: "^%{{ sudo_user }} ALL="
    line: "%{{ sudo_user }} ALL=(ALL) NOPASSWD: ALL"
```
`````

---

#### 🛠️ Usage

1. Set the variable `sudo_user` with the desired username.
2. Run the playbook with the appropriate inventory file:

`````
```bash
ansible-playbook -i inventory.ini playbook.yml --tags sudo
```
`````

---

#### 📋 Requirements

- Ansible 2.9+
- Ubuntu/Debian-based system

---

#### 📄 License

MIT

---

#### 👤 Author

Rajarshi GANGULY

