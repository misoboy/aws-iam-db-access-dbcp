# misoboy/aws-iam-db-access-dbcp

AWS IAM Database Authentication using Apache Common DBCP connection pool

## Installation

```
git clone https://github.com/misoboy/aws-iam-db-access-dbcp.git
```

## Examples

```cmd
mvn clean test -Daws.profile=aws cli profile name
```

## Overview

You need to modify the jdbc connection properties. `application-test.profiles`

```properties
# Region
datasource.rds.region=
# AWS RDS Service Endpoint
datasource.rds.endpoint=
# AWS RDS Service Port
datasource.rds.port=
# AWS RDS Username
datasource.rds.username=
datasource.rds.driverClassName=com.mysql.cj.jdbc.Driver
# AWS RDS JDBC URL
datasource.rds.url=

# Region
datasource.redshift.region=ap-northeast-2
# AWS Redshift Cluster ID
datasource.redshift.clusterId=
# AWS Redshift Username
datasource.redshift.username=
datasource.redshift.driverClassName=com.amazon.redshift.jdbc.Driver
# AWS Redshift JDBC URL
datasource.redshift.url=
```

Enjoy!
