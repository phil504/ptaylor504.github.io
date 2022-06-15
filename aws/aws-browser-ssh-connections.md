---
layout: default
title: AWS Browser SSH Connect
parent: AWS Tips
---
Browser-based SSH connections

Browser-based SSH connections require that your instance's security group inbound rules allow EC2 Instance Connect access to SSH on TCP port 22.

EC2 Instance Connect uses specific IP ranges for browser-based SSH connections to your instance. These IP ranges differ between AWS Regions. To find the AWS IP address range for EC2 Instance Connect in a specific Region, use the following commands:

Note: In the following commands, replace us-east-1 with the AWS Region of your instance.

Windows (requires Windows PowerShell for AWS)

<div class="code-example" markdown="1">
```java
PS C:\> Get-AWSPublicIpAddressRange -Region us-east-1 -ServiceKey EC2_INSTANCE_CONNECT | select IpPrefix
```
</div>

Linux (requires curl and jq)

<div class="code-example" markdown="1">
```java
$ curl -s https://ip-ranges.amazonaws.com/ip-ranges.json| jq -r '.prefixes[] | select(.region=="us-east-1") | select(.service=="EC2_INSTANCE_CONNECT") | .ip_prefix'
```
</div>

Update your security group inbound rules to allow TCP port 22 access from the IP range returned by the preceding commands.

