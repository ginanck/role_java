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



### File: `defaults/main.yml`

| Variable | Default Value | Description |
|----------|---------------|-------------|
| `java_path` | `/opt/java` | None |
| `java_setup` | `binary` | None |
| `java_versions` | `[]` | None |
| `java_versions.0` | `{}` | None |
| `java_versions.0.version` | `8.372.07.1` | None |
| `java_versions.0.filename` | `amazon-corretto-8.372.07.1-linux-x64.tar.gz` | None |
| `java_versions.0.url` | `https://corretto.aws/downloads/resources/8.372.07.1/amazon-corretto-8.372.07.1-linux-x64.tar.gz` | None |
| `java_versions.0.default` | `True` | None |
| `java_versions.1` | `{}` | None |
| `java_versions.1.version` | `11.0.19.7.1` | None |
| `java_versions.1.filename` | `amazon-corretto-11.0.19.7.1-linux-x64.tar.gz` | None |
| `java_versions.1.url` | `https://corretto.aws/downloads/resources/11.0.19.7.1/amazon-corretto-11.0.19.7.1-linux-x64.tar.gz` | None |
| `java_versions.1.users` | `[]` | None |
| `java_versions.1.users.0` | `root` | None |
| `java_versions.2` | `{}` | None |
| `java_versions.2.version` | `17.0.7.7.1` | None |
| `java_versions.2.filename` | `amazon-corretto-17.0.7.7.1-linux-x64.tar.gz` | None |
| `java_versions.2.url` | `https://corretto.aws/downloads/resources/17.0.7.7.1/amazon-corretto-17.0.7.7.1-linux-x64.tar.gz` | None |
| `java_versions.3` | `{}` | None |
| `java_versions.3.version` | `20.0.1.9.1` | None |
| `java_versions.3.filename` | `amazon-corretto-20.0.1.9.1-linux-x64.tar.gz` | None |
| `java_versions.3.url` | `https://corretto.aws/downloads/resources/20.0.1.9.1/amazon-corretto-20.0.1.9.1-linux-x64.tar.gz` | None |




## Task Overview


This role performs the following tasks:


### `install-binary.yml`


- **Create a directory if it does not exist - {{ java.filename }}**
- **Get stats JDK archive - {{ java.filename }}**
- **Download {{ java.filename }}**
- **Unarchive file {{ java.filename }}**
- **Set default Java version**
- **Set JAVA_HOME for users**


### `install-repo.yml`


- **Install OpenJDK from Repository**


### `user-set-java.yml`


- **Get JAVA_HOME for user - {{ user }}**
- **Get user details - {{ user }}**
- **Set Java HOME ~/.bashrc for user - {{ user }}**
- **Set PATH ~/.bashrc for user - {{ user }}**


### `main.yml`


- **Install Java Setup from repository**
- **Install Java Setup from binary archive**




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

## Documentation Maintenance

### Updating Dependencies

1. **Update** `meta/main.yml`:
   ```yaml
   documented_requirements:
     - src: https://github.com/user/role.git
       version: master
     - name: collection.name
       version: 1.0.0
   ```

2. **Sync** `meta/install_requirements.yml` with the same requirements

3. **Regenerate** documentation:
   ```bash
   pre-commit run --all-files
   ```

### Template Updates

- Edit `.docsible_template.md` for structure changes
- Test with: `docsible --role . --md-template .docsible_template.md -nob -com -tl`
- Commit both template and generated README.md

### Quick Checklist

When updating dependencies:
- [ ] Add to `meta/main.yml` → `documented_requirements`
- [ ] Add to `meta/install_requirements.yml`
- [ ] Run `pre-commit run --all-files`
- [ ] Verify generated README.md
- [ ] Commit all changes

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
