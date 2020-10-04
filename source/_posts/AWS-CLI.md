---
title: AWS-CLI
date: 2020-08-30 16:41:53
tags:
---
### 配置AWS CLI
在命令行运行 aws configure 以设置您的证书和设置。
```bash
$ aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-east-2
Default output format [None]: json
```

- AWS 访问密钥 ID 和 AWS 秘密访问密钥 – 这些是您的账户凭证，如果没有，登陆控制台，到用户的认证情报Tag下生成。注意；只能下载一次CSV文件，一定妥善保管。
- 默认区域名称 – 标识默认情况下您要将请求发送到的服务器所在的区域。
- 默认输出格式 – 此格式可以是 json、text 或 table。如果不指定，将使用 json。

配置后的文件保存于

1. CLI 凭证文件 （aws_access_key_id aws_secret_access_key）
~/.aws/credentials（在 Linux, macOS, or Unix 上）
C:\Users\USERNAME.aws\credentials（在 Windows 上）
2. CLI 配置文件（region output）
~/.aws/config（在 Linux, macOS, or Unix 上）
C:\Users\USERNAME.aws\config（在 Windows 上）。

### 配置文件指定
~/.aws/credentials

```bash
[default]
aws_access_key_id=AKIAIOSFODNN7EXAMPLE
aws_secret_access_key=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

[user1]
aws_access_key_id=AKIAI44QH8DHBEXAMPLE
aws_secret_access_key=je7MtGbClwBF/2Zp9Utk/h3yCo8nvbEXAMPLEKEY
```

~/.aws/config

```bash
[default]
region=us-west-2
output=json

[profile user1]
region=us-east-1
output=text
```

#### 使用命名配置文件
请向您的命令添加 --profile profile-name 选项。
未指定时，使用缺省配置。

```bash
aws ec2 describe-instances --profile user1
```

指定区域·/ 指定输出格式·

```bash
$ aws ec2 describe-instances --output table --region us-east-1
```