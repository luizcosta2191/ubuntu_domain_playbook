## Ansible Playbooks to Add Ubuntu to a Domain

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)


This repository contains two playbooks that demonstrate how to perform the following tasks on Ubuntu systems:

- Change the hostname
- Create a local user
- Add to a domain

These playbooks were developed to showcase skills and knowledge in Ansible, serving both as a personal portfolio and as study material for others interested in learning Ansible.

### Monolithic Playbook
The monolithic playbook performs all steps in a single file, along with a separate variables file (vars_ubuntu_domain.yml). This is a simple and straightforward example of how to use Ansible to automate the mentioned tasks. The structure is as follows:

    ├── ubuntu_domain.yml
    └── vars_ubuntu_domain.yml

### Modular Playbook
The modular playbook uses the recommended Ansible structure, separating the logic into roles, handlers, templates, etc. This facilitates maintenance and code reuse. The structure is as follows:

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

## 📄 License

MIT — feel free to use, modify, and distribute.
