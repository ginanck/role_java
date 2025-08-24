# role_java

This Ansible role automates the installation and configuration of multiple Java versions on Linux systems. It supports both binary distribution installation (Amazon Corretto) and repository-based installation, providing flexible Java environment management for development and production environments.

## Features

- Install multiple Java versions simultaneously from binary distributions
- Configure Java alternatives system for version switching
- Set up JAVA_HOME environment variables for specific users
- Support for Amazon Corretto JDK versions 8, 11, 17, and 20
- Repository-based installation option for standard package management
- Automatic download and extraction of Java distributions
- User-specific Java environment configuration

## Requirements

- Target systems must be Linux-based (CentOS, RHEL, Ubuntu, etc.)
- Ansible 2.1 or higher
- Internet connectivity for downloading Java distributions (binary setup)
- sudo privileges on target hosts
- `community.general` collection for alternatives module

## Role Variables

### Installation Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `java_path` | `/opt/java` | Installation directory for Java distributions |
| `java_setup` | `binary` | Installation method: `binary` for distribution files or `repo` for package manager |

### Java Version Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `java_versions` | See below | List of Java versions to install with their configurations |

#### Default Java Versions

```yaml
java_versions:
  - version: 8.372.07.1
    filename: amazon-corretto-8.372.07.1-linux-x64.tar.gz
    url: https://corretto.aws/downloads/resources/8.372.07.1/amazon-corretto-8.372.07.1-linux-x64.tar.gz
    default: true
  - version: 11.0.19.7.1
    filename: amazon-corretto-11.0.19.7.1-linux-x64.tar.gz
    url: https://corretto.aws/downloads/resources/11.0.19.7.1/amazon-corretto-11.0.19.7.1-linux-x64.tar.gz
    users: ["root"]
  - version: 17.0.7.7.1
    filename: amazon-corretto-17.0.7.7.1-linux-x64.tar.gz
    url: https://corretto.aws/downloads/resources/17.0.7.7.1/amazon-corretto-17.0.7.7.1-linux-x64.tar.gz
  - version: 20.0.1.9.1
    filename: amazon-corretto-20.0.1.9.1-linux-x64.tar.gz
    url: https://corretto.aws/downloads/resources/20.0.1.9.1/amazon-corretto-20.0.1.9.1-linux-x64.tar.gz
```

### Repository Installation

| Variable | Default | Description |
|----------|---------|-------------|
| `java_package_name` | Not defined | Package name for repository-based installation (e.g., `java-1.8.0-openjdk`) |

## Dependencies

This role has no dependencies on other Ansible roles.

## Example Playbook

```yaml
---

- name: Install and configure Jenkins
  hosts: jenkins
  become: true
  become_method: sudo
  gather_facts: true
  vars_files:
    - vault/jenkins.yml

  roles:
    - role: role_base
      tags: base
    - role: role_java
      tags: java
    - role: role_tomcat
      tags: tomcat
      when: inventory_hostname in groups['ci_master']
    - role: role_docker
      tags: docker
      when: inventory_hostname in groups['ci_slaves_linux']
    - role: role_jenkins
      tags: jenkins
```

## Configuration

### Ansible Configuration

```ini
[defaults]
remote_user             = ansible
host_key_checking       = False
gathering               = smart
gather_facts            = false
forks                   = 5
collections_paths       = ./collections
roles_path              = ./roles
vault_password_file     = vault/vault_pass.txt
```

## Usage

### 1. Prepare Inventory

```ini
[jenkins:children]
ci_master
ci_slaves

[ci_master]
172.16.2.41 base_hostname=jenkins-master

[ci_slaves:children]
ci_slaves_linux
ci_slaves_windows

[ci_slaves_linux]
172.16.2.42 base_hostname=jenkins-slaves-01
172.16.2.43 base_hostname=jenkins-slaves-02

[ci_slaves_windows]
```

### 2. Run the Playbook

```bash
ansible-playbook -i inventory/jenkins.ini playbooks/jenkins.yml --tags java
```

### 3. Verify Installation

```bash
# Check installed Java versions
sudo alternatives --display java

# Verify Java installation
java -version

# Check JAVA_HOME for specific users
sudo su - root -c 'echo $JAVA_HOME'
```

## Operations

### Adding New Java Versions

To add additional Java versions, extend the `java_versions` list in your playbook or inventory:

```yaml
java_versions:
  - version: 21.0.1.12.1
    filename: amazon-corretto-21.0.1.12.1-linux-x64.tar.gz
    url: https://corretto.aws/downloads/resources/21.0.1.12.1/amazon-corretto-21.0.1.12.1-linux-x64.tar.gz
    default: false
    users: ["jenkins", "developer"]
```

### Switching Default Java Version

Use the alternatives system to switch between installed versions:

```bash
sudo alternatives --config java
```

## License

GPL-2.0-or-later

## Author Information

Gorkem Inanc Korkmaz - NNC Guru
