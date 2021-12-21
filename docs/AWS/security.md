# AWS Security

> [GuardDuty](#GuardDuty)  
> [Macie](#Macie)    
> [WAF](#WAF)  
> [Amazon Inspector](#Amazon_Inspector)  
> [AWS Secrets Manager](#AWS_Secrets_Manager)  

## GuardDuty
- **Amazon GuardDuty is a threat detection service that continuously monitors your AWS accounts and workloads for malicious activity and delivers detailed security findings for visibility and remediation.**
- Intelligent Threat discovery to Protect AWS Account
- Input data includes:
    - CloudTrail Logs: unusual API calls, unauthorized deployments
    - VPC Flow Logs: unusual internal traffic, unusual IP address
    - DNS Logs: compromised EC2 instances sending encoded data within DNS queries


## Macie
- Amazon Macie is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover and **protect your sensitive data in AWS**

## AWS WAF – Web Application Firewall
- Protects your web applications from common web exploits (Layer 7)
- **Layer 7 is HTTP** (vs Layer 4 is TCP)
-  Deploy on **Application Load Balancer, API Gateway, CloudFront**
-  **Define Web ACL (Web Access Control List)**:
    - Rules can include: **IP addresses**, HTTP headers, HTTP body, or URI strings
    - Protects from common attack - SQL injection and Cross-Site Scripting (XSS)
    - Size constraints, **geo-match (block countries)**
    - Rate-based rules (to count occurrences of events) – for DDoS protection

## Amazon Inspector
> **Automated Security Assessments** for EC2 instances


- cf) **AWS Trusted Advisors** provides recommendations that help you follow AWS best practices. Trusted Advisor evaluates your account by using checks. These checks identify ways to optimize your AWS infrastructure, improve security and performance, reduce costs, and monitor service quotas.

## AWS_Secrets_Manager
- Newer service, meant for storing secrets
- Capability to force **rotation of secrets** every X days
- Automate generation of secrets on rotation (uses Lambda)
- Integration with **Amazon RDS** (MySQL, PostgreSQL, Aurora)
- Secrets are encrypted using KMS
- Mostly meant for RDS integration
- [Secrets Manager](https://aws.amazon.com/blogs/security/rotate-amazon-rds-database-credentials-automatically-with-aws-secrets-manager/)