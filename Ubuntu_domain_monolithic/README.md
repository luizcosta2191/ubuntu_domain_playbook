# Ansible Playbook: Join Ubuntu to Domain (monolithic playbook)

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
-
This repository contains an Ansible playbook for adding an Ubuntu machine to an Active Directory domain. The playbook performs a series of tasks including configuring the hostname, installing necessary packages, configuring configuration files, and joining the machine to the domain.

### Requirements

 - Ansible 2.9 or higher
 - Ubuntu 18.04 or higher
 - Access to an Active Directory domain


## Playbook Structure

- **Change Hostname:** Updates the machine's hostname.
- **Create Local User:** Adds a new local user.
- **Install Packages:** Installs necessary packages for AD integration.
- **Configure krb5.conf:** Configures the Kerberos configuration file.
- **Update PAM:** Updates PAM configuration.
- **Join Domain:** Joins the machine to the Active Directory domain.
- **Configure sssd.conf:** Configures SSSD for authentication.
- **Restart SSSD Service:** Restarts the SSSD service.
- **Reboot Machine:** Reboots the machine to apply all changes.


### File Descriptions:

 - **ubuntu_domain.yml**: The main playbook file.
 - **vars_ubuntu_domain.yml**: Variable file containing sensitive and environment-specific information.



## Usage Instructions

### Step 1: Clone the Repository

Clone the repository to your local machine:

    git clone https://github.com/luizcosta2191/Ubuntu_domain_playbook.git
    cd Ubuntu_domain-playbook/Ubuntu_domain_monolithic



### Step 2: Configure Variables

Edit the vars_ubuntu_domain.yml file with your environment-specific information:


```yaml
    hostname: "hostname"
    user_local: "local machine user"
    password: "local machine user's password"
    domain_upper: "uppercase domain address"
    domain_lower: "lowercase domain address"
    admin_user: "Active Directory admin user"
    admin_pass: "Active Directory admin password"
    domain_component: "domain component"
```


### Step 3: Protect Sensitive Variables

Use Ansible Vault to encrypt the variable file:



    ansible-vault encrypt vars_ubuntu_domain.yml



### Step 4: Run the Playbook

Run the playbook with the following command:



    ansible-playbook -i hosts ubuntu_domain.yml --ask-vault-pass



### Step 5: Verify

After execution, verify that the machine has been successfully added to the domain and all configurations have been applied.


## 📄 License

MIT — feel free to use, modify, and distribute.
