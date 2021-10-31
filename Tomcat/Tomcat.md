# Installing and configuring `tomcat`
---

### Installing `tomcat`
---
> wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.54/bin/apache-tomcat-9.0.54.tar.gz
> tar -zxvf apache-tomcat-9.0.54.tar.gz

---
---

### Setting-up `tomcat`
---
* Create role and user
    ```xml
        ...
        <role rolename="manager-gui"/>
        <role rolename="manager-script"/>
        <role rolename="manager-jmx"/>
        <role rolename="manager-status"/>
        <user username="<<user-name>>" password="<<password>>" roles="<<rolename>>"/>
        ...
        ...
    ```
* Config change to enable UI access
    > export tomcat_path=/opt/tomcat
    > find $tomcat_path -name context.xml
    comment the section in all the `context.xml` files within the `webapp` folder
    > <Valve className .../>
* restart `tomcat`

---
---