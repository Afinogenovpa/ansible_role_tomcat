## [Tomcat ansible role](#tomcat-ansible-role) 
[![Version](https://img.shields.io/github/v/release/afinogenovpa/ansible_role_tomcat)](https://github.com/Afinogenovpa/ansible_role_tomcat/releases/)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-afinogenovpa.tomcat-green)](https://galaxy.ansible.com/afinogenovpa/tomcat)

> Install and configure apache Tomcat on your system(RedHat, Arch, Debian Linux).
- [Installation](#installation)
- [Role variables](#role-variables)
- [How to run playbook](#running-playbook)
- [Tested on](#tested-on-the-following-operating-systems) 
- [Author](#author-information)

## [Installation](#installation)
#### Ansible galaxy
```
ansible-galaxy install afinogenovpa.tomcat
```

#### Manual install
- Clone the Project:

```
$ git clone https://github.com/Afinogenovpa/ansible_role_tomcat.git
$ cd ansible_role_tomcat/
$ mkdir -p roles/tomcat
$ mv defaults/ handlers/ meta/ tasks/ templates/ vars/ roles/tomcat/
```

- Update your inventory:
```
$ vim hosts
[tomcat_nodes]
127.0.0.1 - change if you need a non-local installation
```

- Update variables in playbook file 
```
- name: Tomcat playbook
  hosts: tomcat_nodes       # Inventory hosts group / server to act on
  connection: local         # Delete if you need a non-local installation
  become: yes               # If to escalate privilege
  become_method: sudo       # Set become method
  remote_user: root         # Update username for remote server
  vars:
    tomcat_version: "9.0.73"
    tomcat_user: tomcat
    tomcat_group: tomcat
    tomcat_install_dir: "/opt"
    tomcat_install_java: true
    java_package: "openjdk-17-jdk"
    force_tomcat_install: false
    clean_tomcat_downloaded: false
    tomcat_manager:                 # Delete this section if you don't need tomcat manager, will be setup default values
      host_manager_allow: ".*"
      manager_allow: ".*"
      roles:
        - rolename: "manager-gui"
      users:
        - username: "tomcat"
          password: "tomcat"
          roles: "manager-gui"
    server:                         # Delete this section if you don't need server custom opts
      host: "localhost"
      address: "0.0.0.0"
      port: 8080
      timeout: 20000
      max_post_size: 209715200
      redirect_port: 8443
      auto_deployment: true 
    set_env:                        # Delete this section if you don't need custom opts
      - 'JAVA_OPTS="-Xms512M -Xmx512M"'
  roles:
    - tomcat
```

If you are using non root remote user, then set username and enable sudo:

```
become: yes
become_method: sudo
```

## [Role Variables](#role-variables)
The minimum of default values for the variables are set in [`defaults/main.yml`](https://github.com/Afinogenovpa/Tomcat_install_ansible_role/blob/main/defaults/main.yml):

```
tomcat_version: "9.0.73" - setup this version
```

#### JAVA setup
```
tomcat_install_java: true - set true for setup java package from packet manager, it works on Debian,Arch,Redhat OS
java_package: "openjdk-17-jdk" - Ubuntu 20.04.5 LTS example
java_home: "" - if necessary
```

#### Creates user and group on server
```
tomcat_user: tomcat
tomcat_group: tomcat
```

#### "tomcat_install_dir" the following folders will be created in this directory: apache-tomcat-"tomcat_version" dir and "tomcat" symbolic link to the apache-tomcat-"tomcat_version" folder
```
tomcat_install_dir: "/opt"
```

#### "clean_tomcat_downloaded", if the value of the variable is true, then dowloaded Tomcat arhive in "/tmp/" will be deleted after extract
```
clean_tomcat_downloaded: false
```

#### "force_tomcat_install", if the value of the variable is true, then the all Tomcat versions in "tomcat_install_dir" will be deleted, and after that the Tomcat will be installed from scratch. Use carefully.
```
force_tomcat_install: false
```

#### "tomcat_manager", use to fill the config file tomcat-users.xml, not required to use
```
tomcat_manager:
  host_manager_allow: ".*" - by default it is "127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" - localhost
  manager_allow: ".*" - by default it is "127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" - localhost
  roles:
  - rolename: "manager-gui"
  users:
  - username: "tomcat"
    password: "tomcat"
    roles: "manager-gui"
```

#### "server", use to fill the config file server.xml, not required to use
```
server:
  host: "localhost"
  address: "0.0.0.0"
  port: 8080
  timeout: 20000
  max_post_size: 209715200
  redirect_port: 8443
  auto_deployment: true 
```

#### "set_env", use to fill the config file setenv.sh, not required to use
```
set_env:
 - 'JAVA_OPTS="-Xms512M -Xmx512M"'
```

## [Running Playbook](#running-playbook)

```
ansible-playbook -i hosts.ini tomcat_playbook.yml
```

## [Tested on the following operating systems](#tested-on-the-following-operating-systems) 
- Ubuntu 20.04 / Ubuntu 18.04

## [Author Information](#author-information)
soon...
