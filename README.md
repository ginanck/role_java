Role Name
=========

role_pve_template

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

The following variables are set in defaults/main.yml and can be overridden:

- `java_path`: The path to install Java on the system. The default is `/opt/java`.
- `java_setup`: The setup method to install Java. The default is `binary`.
- `java_versions`: A list of Java versions to install. Each version is a dictionary that includes:
    - `version`: The version of Java.
    - `filename`: The filename of the Java distribution to download.
    - `url`: The URL to download the Java distribution.
    - `default`: (Optional) A boolean that indicates if this is the default Java version. The default is `true`.
    - `users`: (Optional) A list of users for this Java version.

For example:

```yml
java_versions:
  - version: 8.372.07.1
    filename: amazon-corretto-8.372.07.1-linux-x64.tar.gz
    url: https://corretto.aws/downloads/resources/8.372.07.1/amazon-corretto-8.372.07.1-linux-x64.tar.gz
    default: true
  - version: 11.0.19.7.1
    filename: amazon-corretto-11.0.19.7.1-linux-x64.tar.gz
    url: https://corretto.aws/downloads/resources/11.0.19.7.1/amazon-corretto-11.0.19.7.1-linux-x64.tar.gz
    users: ["ansible"]
```

Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yml
- hosts: servers
  roles:
     - { role: username.role_pve_template, java_path: '/opt/java' }
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
