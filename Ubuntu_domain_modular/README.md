# Ansible Playbook: Adding Ubuntu to a Domain (modular playbook)

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

This repository contains a modular playbook for adding an Ubuntu machine to an Active Directory domain. The playbook performs a series of tasks, including configuring the hostname, creating a local user, installing necessary packages, configuring configuration files, and joining the machine to the domain.

## Requirements
- Ansible 2.9 or higher
- Ubuntu 18.04 or higher
- Access to an Active Directory domain

## Directory Structure
```bash
ubuntu_domain_modular/
├── ubuntu_domain.yml
├── group_vars/
│   └── linux/
│       ├── change_hostname.yml
│       ├── local_user.yml
│       ├── install_packages.yml
│       └── domain_join.yml
└── roles/
    ├── change_hostname/
    │   └── tasks/
    │       └── main.yml
    ├── local_user/
    │   └── tasks/
    │       └── main.yml
    ├── install_packages/
    │   └── tasks/
    │       └── main.yml
    └── domain_join/
        ├── meta/
        │   └── main.yml
        ├── tasks/
        │   └── main.yml
        ├── handlers/
        │   └── main.yml
        └── templates/
            ├── krb5.conf.j2
            └── sssd.conf.j2
```
### File Descriptions

-   **ubuntu_domain.yml**: The main playbook file that orchestrates the tasks and roles.

-   **group_vars/**: Directory containing variable files specific to the environment.

    -   `change_hostname.yml`: Variables for changing the hostname.
    -   `local_user.yml`: Variables for creating a local user.
    -   `install_packages.yml`: Variables for package installation.
    -   `domain_join.yml`: Variables for joining the domain.
-   **roles/**: Directory containing role-specific tasks, handlers, and templates.

    -   **change_hostname/**:
        -   `tasks/main.yml`: Task file for changing the machine's hostname.
    -   **local_user/**:
        -   `tasks/main.yml`: Task file for creating a local user.
    -   **install_packages/**:
        -   `tasks/main.yml`: Task file for installing necessary packages.
    -   **domain_join/**:
        -   `meta/main.yml`: Role dependencies.
        -   `tasks/main.yml`: Task file for domain join and configuration.
        -   `handlers/main.yml`: Handlers for service restarts.
        -   **templates/**:
            -   `krb5.conf.j2`: Template for Kerberos configuration.
            -   `sssd.conf.j2`: Template for SSSD configuration.

## Playbook Structure
- **Hostname Change**: Updates the machine's hostname.
- **Local User Creation**: Adds a new local user.
- **Package Installation**: Installs packages needed for AD integration.
- **krb5.conf Configuration**: Configures the Kerberos configuration file.
- **PAM Update**: Updates PAM configurations.
- **Domain Join**: Joins the machine to the Active Directory domain.
- **sssd.conf Configuration**: Configures SSSD for authentication.
- **SSSD Service Restart**: Restarts the SSSD service.
- **Machine Reboot**: Reboots the machine to apply all changes.

## Usage Instructions

### Step 1: Clone the Repository

Clone the repository to your local machine:

```bash
git clone https://github.com/luizcosta2191/Ubuntu_domain_playbook.git
cd Ubuntu_domain-playbook/Ubuntu_domain_modular
  ```

### Step 2: Configure Variables

Edit the files in `group_vars/linux/` with the specific information for your environment:
-   change_hostname.yml
  ```yaml
  hostname: "hostname"
  ```
-   local_user.yml

  ```yaml
user_local: "local machine user"
password: "local machine user's password"
```

-   domain_join.yml

 ```yaml   
 domain_upper: "uppercase domain address"
 domain_lower: "lowercase domain address"
 admin_user: "Active Directory admin user"
 admin_pass: "Active Directory admin password"
 domain_component: "domain component"
 ```
### Step 3: Secure Sensitive Variables

Use Ansible Vault to secure the variable files:

    ansible-vault encrypt group_vars/linux/*.yml

### Step 4: Run the Playbook

Run the playbook with the command:

    ansible-playbook -i hosts ubuntu_domain.yml --ask-vault-pass

### Step 5: Verify

After execution, verify that the machine has been correctly added to the domain and that all configurations have been applied.

## 📄 License

MIT — feel free to use, modify, and distribute.

