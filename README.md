# Tomcat ansible role


:warning: **java must be installed before using this role** :warning:

```
tomcat_release: "9"
tomcat_version: "9.0.73"
tomcat_url: "https://downloads.apache.org/tomcat/tomcat-{{ tomcat_release }}/v{{ tomcat_version}}/bin/apache-tomcat-{{ tomcat_version }}.tar.gz" 
```

#### Write path JAVA_HOME
```
java_home: ""
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
  host_manager_allow: ".*" - by default it is "127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1"
  manager_allow: ".*" - by default it is "127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1"
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
