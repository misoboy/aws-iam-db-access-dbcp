# misoboy/aws-iam-db-access-dbcp

AWS IAM Database Authentication using Apache Common DBCP connection pool

## Installation

```
git clone https://github.com/misoboy/aws-iam-db-access-dbcp.git
```

## Overview

AWS RDS, Redshift IAM Access authentication method is applied to Apache Common DBCP to create a token when a connection pool is created, and connect to the database.

This source code is compatible with Apache Common DBCP versions v1, v2.

## Usage

The example is implemented as a Junit Test case to create a Connection.

You need to modify the jdbc connection properties. `test/resources/application-test.properties`

```properties
# Region
datasource.rds.region=ap-northeast-2
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

Set AWS CLI authentication information for your environment.

Edit `$USER_HOME/.aws/config`.
```
[default]
output = json
region = ap-northeast-2

[my-profile]
output = json
region = ap-northeast-2
```

Edit `$USER_HOME/.aws/credentials`.
```
[default]
aws_access_key_id = ...
aws_secret_access_key = ...

[my-profile]
aws_access_key_id = ...
aws_secret_access_key = ...
```

Go to the project workspace root path.
Run Maven Junit Test case.

```cmd
$ mvn clean test -Daws.profile=If omitted, the default profile is used.
```
