Simple role to install AWS-Cli
=========

This role installs the AWS Cli

To define the users in the credentials file, describe the user and his credentials in the default profile.  
The role will create the .aws/credentials file in the user home folder.

```yaml
awscli_users:
  backup:  # user
    default:  # profile
      aws_access_key_id: changeme  # key definition
      aws_secret_access_key: changeme
```

You can define more than user or profiles and configurations per profile.  
The definitions on config variable will be populating data in the .aws/config file
```yaml
awscli_users:
  backup:  # user
    default:  # profile
      aws_access_key_id: changeme  # key definition
      aws_secret_access_key: changeme
    user:  # profile
      aws_access_key_id: changeme  
      aws_secret_access_key: changeme
      config:  # config definition
        region: us-west-1
        output: json
```

## Author Information
- Dorance Martinez @dorancemc
