# 🌍 Environment Substitution Repository

[![GitHub stars](https://img.shields.io/github/stars/bkona-alopa/test-env-sub-321?style=flat-square)](https://github.com/bkona-alopa/test-env-sub-321)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)
[![Last Updated](https://img.shields.io/badge/updated-May%202026-brightgreen.svg?style=flat-square)](README.md)

> A comprehensive toolkit for managing dynamic environment substitution across multiple deployment environments.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [What is Environment Substitution?](#what-is-environment-substitution)
- [Key Features](#key-features)
- [Use Cases](#use-cases)
- [How It Works](#how-it-works)
- [Common Variable Types](#common-variable-types)
- [Best Practices](#best-practices)
- [Integration with Infrastructure as Code](#integration-with-infrastructure-as-code)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Contributing](#contributing)
- [Support](#support)
- [License](#license)

---

## 🎯 Overview

This repository is dedicated to managing **environment substitution** - a powerful process that dynamically replaces configuration variables and values based on the target deployment environment (development, staging, QA, UAT, production, etc.).

**Key Benefit**: Deploy the same codebase across multiple environments without manual configuration changes!

---

## ❓ What is Environment Substitution?

Environment substitution is a technique used to automatically replace placeholders or variables in configuration files with actual values specific to each environment. This allows a single codebase to be deployed across multiple environments without manual modifications.

### Why Use It?

✅ **Consistency**: Same code, same configuration templates across all environments  
✅ **Automation**: Reduce manual errors through automated variable replacement  
✅ **Security**: Keep sensitive data separate from source code  
✅ **Scalability**: Easily add new environments without code changes  

---

## ⚡ Key Features

| Feature | Description |
|---------|-------------|
| 🔄 **Dynamic Configuration** | Replace environment-specific values at deployment time |
| 🌐 **Multi-Environment Support** | Handle dev, staging, QA, UAT, and production seamlessly |
| 🔐 **Security First** | Keep sensitive data out of version control using environment variables |
| ☁️ **Infrastructure Flexibility** | Support for various cloud providers and on-premise deployments |
| 📝 **Template-Based** | Use configuration templates with variable placeholders |
| ✔️ **Validation** | Verify all required variables are substituted |

---

## 📌 Use Cases

1. **🗄️ Database Configuration**  
   Swap database endpoints, credentials, and connection pools based on environment

2. **🌐 API Endpoints**  
   Use different API URLs and base paths for different environments

3. **🔑 Secrets Management**  
   Inject API keys, tokens, passwords, and certificates at runtime

4. **📦 Resource Naming**  
   Update AWS S3 buckets, RDS instances, VPCs, and other resources per environment

5. **📊 Logging and Monitoring**  
   Configure different log levels, monitoring tools, and alerting thresholds

6. **⚙️ Feature Flags**  
   Enable/disable features based on environment

---

## 🚀 How It Works

### Example Workflow

**Step 1: Create a Template**
```bash
# config.template.env
DATABASE_HOST=${DB_HOST}
DATABASE_PORT=${DB_PORT}
API_ENDPOINT=${API_URL}
LOG_LEVEL=${LOG_LEVEL}
SECRET_KEY=${SECRET_KEY}
```

**Step 2: Define Environment Variables**
```bash
# .env.production
DB_HOST=prod-db.aws.amazon.com
DB_PORT=5432
API_URL=https://api.production.example.com
LOG_LEVEL=error
SECRET_KEY=prod-secret-key-12345
```

**Step 3: Perform Substitution**
```bash
envsubst < config.template.env > config.production.env
```

**Step 4: Result**
```bash
# config.production.env (after substitution)
DATABASE_HOST=prod-db.aws.amazon.com
DATABASE_PORT=5432
API_ENDPOINT=https://api.production.example.com
LOG_LEVEL=error
SECRET_KEY=prod-secret-key-12345
```

### Available Substitution Tools

- **envsubst**: Built-in Unix tool for environment variable substitution
- **Terraform**: Native variable interpolation and tfvars files
- **Docker Compose**: Environment variable substitution in compose files
- **Kubernetes**: ConfigMaps and Secrets for dynamic configuration
- **Custom Scripts**: Shell, Python, or Go-based substitution engines

---

## 📦 Common Variable Types

### Infrastructure Variables
- Hostnames and domain names
- IP addresses and port numbers
- Region and availability zones
- Instance types and sizes

### Application Variables
- Feature flags and toggles
- Timeout values and retry counts
- Batch sizes and rate limits
- Cache TTL and memory limits

### Security Variables
- Database passwords and usernames
- API keys and tokens
- SSL certificates and private keys
- OAuth credentials

### Deployment Variables
- Environment identifiers (dev, prod, etc.)
- Deployment regions
- Replica counts
- Resource quotas

---

## ✅ Best Practices

### 1. **Never Commit Secrets** 🔒
```bash
❌ WRONG: DATABASE_PASSWORD=my-secret-123
✅ RIGHT: Use environment variable files outside the repo or vault services
```

### 2. **Use Consistent Naming Conventions**
```bash
✅ Good: DB_HOST, API_URL, LOG_LEVEL
❌ Bad: database, api, logging
```

### 3. **Document All Variables**
Create a `.env.example` file listing all required variables:
```bash
# .env.example
DATABASE_HOST=
DATABASE_PORT=
API_ENDPOINT=
LOG_LEVEL=
```

### 4. **Validate Substitution**
Ensure all required variables are provided before deployment:
```bash
#!/bin/bash
required_vars=("DB_HOST" "API_URL" "LOG_LEVEL")
for var in "${required_vars[@]}"; do
  if [ -z "${!var}" ]; then
    echo "ERROR: $var is not set"
    exit 1
  fi
done
```

### 5. **Test Each Environment**
Verify substitution occurred correctly before deploying to production.

### 6. **Version Your Configuration Templates**
Keep track of changes to configuration templates:
```bash
templates/
├── v1.0/
├── v1.1/
└── v2.0/
```

### 7. **Use Secret Management Services**
- AWS Secrets Manager
- HashiCorp Vault
- Azure Key Vault
- Kubernetes Secrets

---

## 🔗 Integration with Infrastructure as Code

### Terraform Example

```hcl
# variables.tf
variable "db_host" {
  type        = string
  description = "Database hostname"
}

variable "instance_type" {
  type        = string
  default     = "t3.micro"
}

# main.tf
resource "aws_db_instance" "main" {
  engine               = "postgres"
  instance_class       = var.instance_type
  allocated_storage    = 20
  username             = "admin"
  password             = var.db_password
  db_name              = "production"
  skip_final_snapshot  = false
  
  tags = {
    Name        = "prod-db"
    Environment = "production"
  }
}

# terraform.tfvars (for production)
db_host     = "prod-db.aws.amazon.com"
instance_type = "db.t3.small"
db_password = "secure-password-here"
```

### CloudFormation Example

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Parameters:
  DBHost:
    Type: String
    Description: Database hostname
  Environment:
    Type: String
    AllowedValues: [dev, staging, production]

Resources:
  AppServer:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0c55b159cbfafe1f0
      InstanceType: t3.micro
      Environment:
        - Name: DATABASE_HOST
          Value: !Ref DBHost
        - Name: ENV
          Value: !Ref Environment
```

---

## 📂 Repository Structure

```
test-env-sub-321/
├── README.md                          # This file
├── .env.example                       # Template for environment variables
├── LICENSE                            # License file
├── CHANGELOG.md                       # Version history
│
├── environments/                      # Environment-specific configurations
│   ├── dev/
│   │   ├── config.env
│   │   └── secrets.env
│   ├── staging/
│   ├── qa/
│   ├── uat/
│   └── prod/
│
├── templates/                         # Configuration templates with variables
│   ├── database.template.env
│   ├── application.template.env
│   └── services.template.env
│
├── scripts/                           # Substitution and deployment scripts
│   ├── substitute.sh                  # Main substitution script
│   ├── validate.sh                    # Validation script
│   └── deploy.sh                      # Deployment automation
│
└── docs/                              # Additional documentation
    ├── SETUP.md                       # Setup instructions
    ├── TROUBLESHOOTING.md             # Common issues
    └── EXAMPLES.md                    # Usage examples
```

---

## 🎬 Getting Started

### Prerequisites
- Bash shell (or compatible)
- `envsubst` utility (for basic substitution)
- Git

### Quick Start

1. **Clone this repository**
   ```bash
   git clone https://github.com/bkona-alopa/test-env-sub-321.git
   cd test-env-sub-321
   ```

2. **Copy the example environment file**
   ```bash
   cp .env.example .env.dev
   ```

3. **Edit with your environment values**
   ```bash
   nano .env.dev
   ```

4. **Run substitution**
   ```bash
   source .env.dev
   ./scripts/substitute.sh templates/database.template.env > database.env
   ```

5. **Verify the output**
   ```bash
   cat database.env
   ```

6. **Deploy using the generated configuration**
   ```bash
   ./scripts/deploy.sh database.env
   ```

---

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes and test across multiple environments
4. Commit your changes (`git commit -m 'Add amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-feature`)
6. Open a Pull Request with a clear description

### Code of Conduct
Please be respectful and constructive in all interactions.

---

## 💬 Support

Have questions or need help?

- 📖 Check [TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)
- 🐛 [Report an issue](https://github.com/bkona-alopa/test-env-sub-321/issues)
- 💭 Start a [discussion](https://github.com/bkona-alopa/test-env-sub-321/discussions)
- 📧 Contact the infrastructure team

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📚 Additional Resources

- [Terraform Variables Documentation](https://www.terraform.io/docs/language/values/variables.html)
- [Environment Variables Best Practices](https://12factor.net/config)
- [Docker Environment Variables](https://docs.docker.com/compose/environment-variables/)
- [Kubernetes ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)

---

<div align="center">

**⭐ If you find this helpful, please give it a star!**

Made with ❤️ by the Infrastructure Team

**Last Updated**: May 2026

</div>
