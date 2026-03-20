# aws-iam-db-access-dbcp

> AWS IAM Database Authentication integrated with **Apache Commons DBCP** connection pool — supports RDS and Redshift with automatic token refresh on DBCP v1 and v2.

[![Java](https://img.shields.io/badge/Java-8+-orange?logo=java&logoColor=white)](https://java.com)
[![AWS](https://img.shields.io/badge/AWS-RDS%20%7C%20Redshift-FF9900?logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![DBCP](https://img.shields.io/badge/Apache_Commons-DBCP_v1%2Fv2-red)](https://commons.apache.org/proper/commons-dbcp/)

## Overview

AWS RDS and Redshift support **IAM Database Authentication** — instead of a static password, you use a temporary token generated from AWS IAM credentials. This project integrates that token generation into Apache Commons DBCP so that:

1. A new IAM auth token is generated when the connection pool initializes
2. The token is automatically refreshed before it expires (every 15 minutes)
3. Compatible with **DBCP v1** and **DBCP v2**

## How It Works

```
DBCP Connection Pool
    └─► Custom DataSource wrapper
              └─► AWS SDK GenerateDbAuthToken()
                      └─► Uses IAM Role / Access Key
                              └─► Connect to RDS / Redshift
```

## Getting Started

```bash
git clone https://github.com/misoboy/aws-iam-db-access-dbcp.git
cd aws-iam-db-access-dbcp
./mvnw clean test
```

## Configuration

Update `src/test/resources/application-test.properties`:

```properties
# AWS Region
datasource.rds.region=ap-northeast-2
# RDS Endpoint
datasource.rds.endpoint=your-db.cluster-xxx.ap-northeast-2.rds.amazonaws.com
# RDS Port
datasource.rds.port=3306
# DB Username (must have rds_iam role)
datasource.rds.username=db_user
```

## AWS IAM Setup

The IAM user/role must have the `rds-db:connect` permission:

```json
{
  "Effect": "Allow",
  "Action": "rds-db:connect",
  "Resource": "arn:aws:rds-db:ap-northeast-2:123456789:dbuser:*/db_user"
}
```

## License

MIT
