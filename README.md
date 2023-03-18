# [Tomcat ansible role](#Tomcat-ansible-role) 
Install and configure apache Tomcat on your system.


## [Role Variables](#role-variables)
The default values for the variables are set in [`defaults/main.yml`](https://github.com/Afinogenovpa/Tomcat_install_ansible_role/blob/main/defaults/main.yml):

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
## [Author Information](#author-information)

soon...
