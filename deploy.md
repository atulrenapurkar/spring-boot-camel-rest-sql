### Add MySQL template
    oc create -f https://raw.githubusercontent.com/openshift/origin/master/examples/db-templates/mysql-ephemeral-template.json
    
### Create MySQL
    oc new-app --template=mysql-ephemeral
    
### Create Quartz2 tables

    ./src/main/resources/quartz/tables_mysql.sql

### Deploy
    mvn clean package fabric8:deploy -Dmaven.test.skip=true -Popenshift

### URL
    
    http://spring-boot-camel-rest-sql-fuse7.6923.rh-us-east-1.openshiftapps.com/camel-rest-sql/books
    http://spring-boot-camel-rest-sql-fuse7.6923.rh-us-east-1.openshiftapps.com/camel-rest-sql/books/order/1
    
### UnDeploy
    mvn fabric8:undeploy -Popenshift
    
### Run locally

    mvn clean package spring-boot:run -Dmaven.test.skip=true   

### MySQL
    oc get pods
    oc port-forward mysql-1-xg5kq 3306:3306

    db user: user33I
    db pwd: lwkhDYGriyoEFvBS

### H2

    http://localhost:8080/h2-console