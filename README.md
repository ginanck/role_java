<!-- DOCSIBLE START -->
# Ansible Role: role_java


role_java to setup java


## Table of Contents

- [Requirements](#requirements)
- [Dependencies](#dependencies)
- [Role Variables](#role-variables)
- [Task Overview](#task-overview)
- [Example Playbook](#example-playbook)
- [Documentation Maintenance](#documentation-maintenance)
- [License](#license)
- [Author Information](#author-information)

## Requirements



- Ansible >= 2.9


- Supported platforms:
  - Ubuntu (noble)
  - AlmaLinux (8)



## Dependencies


This role requires the following roles and collections:




  
    
  

  
    
  

  
    
  

  
    
  



**Roles:**

- [role_base](https://github.com/ginanck/role_base.git) (version: master)




**Collections:**

- `community.docker` (>= 4.8.1)

- `community.general` (>= 6.6.1)

- `ansible.posix` (>= 1.5.4)



To install all dependencies:
```bash
ansible-galaxy install -r meta/install_requirements.yml
```


## Role Variables

**These are static variables with lower priority**



#### File: defaults/main.yml

| Var | Type | Value |
|-----|------|-------|
| [java_path](defaults/main.yml#L4) | str | `/opt/java` |
| [java_setup](defaults/main.yml#L5) | str | `binary` |
| [java_versions](defaults/main.yml#L7) | list |  |
| [java_versions.0](defaults/main.yml#L8) | dict |  |
| [java_versions.0.default](defaults/main.yml#L11) | bool | `True` |
| [java_versions.0.filename](defaults/main.yml#L9) | str | `amazon-corretto-8.372.07.1-linux-x64.tar.gz` |
| [java_versions.0.url](defaults/main.yml#L10) | str | `https://corretto.aws/downloads/resources/8.372.07.1/amazon-corretto-8.372.07.1-linux-x64.tar.gz` |
| [java_versions.0.version](defaults/main.yml#L8) | str | `8.372.07.1` |
| [java_versions.1](defaults/main.yml#L12) | dict |  |
| [java_versions.1.filename](defaults/main.yml#L13) | str | `amazon-corretto-11.0.19.7.1-linux-x64.tar.gz` |
| [java_versions.1.url](defaults/main.yml#L14) | str | `https://corretto.aws/downloads/resources/11.0.19.7.1/amazon-corretto-11.0.19.7.1-linux-x64.tar.gz` |
| [java_versions.1.users](defaults/main.yml#L15) | list |  |
| [java_versions.1.users.0](defaults/main.yml#L15) | str | `root` |
| [java_versions.1.version](defaults/main.yml#L12) | str | `11.0.19.7.1` |
| [java_versions.2](defaults/main.yml#L16) | dict |  |
| [java_versions.2.filename](defaults/main.yml#L17) | str | `amazon-corretto-17.0.7.7.1-linux-x64.tar.gz` |
| [java_versions.2.url](defaults/main.yml#L18) | str | `https://corretto.aws/downloads/resources/17.0.7.7.1/amazon-corretto-17.0.7.7.1-linux-x64.tar.gz` |
| [java_versions.2.version](defaults/main.yml#L16) | str | `17.0.7.7.1` |
| [java_versions.3](defaults/main.yml#L19) | dict |  |
| [java_versions.3.filename](defaults/main.yml#L20) | str | `amazon-corretto-20.0.1.9.1-linux-x64.tar.gz` |
| [java_versions.3.url](defaults/main.yml#L21) | str | `https://corretto.aws/downloads/resources/20.0.1.9.1/amazon-corretto-20.0.1.9.1-linux-x64.tar.gz` |
| [java_versions.3.version](defaults/main.yml#L19) | str | `20.0.1.9.1` |




## Task Overview


This role performs the following tasks:


### File: `tasks/install-binary.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Create a directory if it does not exist - {{ java.filename }}](tasks/install-binary.yml#L) | ansible.builtin.file | No | N/A |
| [Get stats JDK archive - {{ java.filename }}](tasks/install-binary.yml#L) | ansible.builtin.stat | No | N/A |
| [Download {{ java.filename }}](tasks/install-binary.yml#L) | ansible.builtin.get_url | Yes | N/A |
| [Unarchive file {{ java.filename }}](tasks/install-binary.yml#L) | ansible.builtin.unarchive | No | N/A |
| [Set default Java version](tasks/install-binary.yml#L) | community.general.alternatives | Yes | N/A |
| [Set JAVA_HOME for users](tasks/install-binary.yml#L) | ansible.builtin.include_tasks | Yes | N/A |




### File: `tasks/install-repo.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Install OpenJDK from Repository](tasks/install-repo.yml#L) | ansible.builtin.yum | No | N/A |




### File: `tasks/user-set-java.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Get JAVA_HOME for user - {{ user }}](tasks/user-set-java.yml#L) | ansible.builtin.shell | No | N/A |
| [Get user details - {{ user }}](tasks/user-set-java.yml#L) | ansible.builtin.getent | No | N/A |
| [Set Java HOME ~/.bashrc for user - {{ user }}](tasks/user-set-java.yml#L) | ansible.builtin.lineinfile | No | N/A |
| [Set PATH ~/.bashrc for user - {{ user }}](tasks/user-set-java.yml#L) | ansible.builtin.lineinfile | No | N/A |




### File: `tasks/main.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Install Java Setup from repository](tasks/main.yml#L) | ansible.builtin.import_tasks | Yes | N/A |
| [Install Java Setup from binary archive](tasks/main.yml#L) | ansible.builtin.include_tasks | Yes | N/A |






## Example Playbook

```yaml
---
- hosts: all
  become: yes
  roles:
    - role: role_java

      vars:
        java_path: /opt/java
        java_setup: binary
        java_versions: []

```

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
