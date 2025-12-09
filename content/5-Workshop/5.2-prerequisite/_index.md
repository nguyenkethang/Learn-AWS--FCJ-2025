---
title: "Prerequisites & Preparation"
date: 2025-12-08
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

## System Requirements

### 1. AWS Account
- Active AWS account
- Administrator access or the following permissions:
  - CloudFormation: Full access
  - EC2: Full access
  - VPC: Full access
  - RDS: Full access
  - S3: Full access
  - CloudFront: Full access
  - IAM: Create roles and policies
  - CloudWatch: Full access

### 2. AWS CLI
Install and configure AWS CLI:

**Windows:**
```powershell
# Download and install from: https://aws.amazon.com/cli/
# Or use chocolatey:
choco install awscli

# Verify installation
aws --version
```

**Linux/Mac:**
```bash
# Using pip
pip install awscli

# Or use package manager
# Ubuntu/Debian
sudo apt-get install awscli

# MacOS
brew install awscli

# Verify installation
aws --version
```

**Configure AWS CLI:**
```bash
aws configure
# AWS Access Key ID: <your-access-key>
# AWS Secret Access Key: <your-secret-key>
# Default region name: ap-southeast-1
# Default output format: json
```

### 3. EC2 Key Pair

Create an EC2 Key Pair for SSH access:

**Via AWS Console:**
1. Open [EC2 Console](https://console.aws.amazon.com/ec2/)
2. Select region **ap-southeast-1** (Singapore)
3. Go to **Network & Security** → **Key Pairs**
4. Click **Create key pair**
5. Name: `workshop-aws-key`
6. Key pair type: **RSA**
7. Private key file format: **.pem** (Linux/Mac) or **.ppk** (Windows/PuTTY)
8. Click **Create key pair**
9. Save the `.pem` file securely

**Via AWS CLI:**
```bash
# Create key pair
aws ec2 create-key-pair \
  --key-name workshop-aws-key \
  --query 'KeyMaterial' \
  --output text \
  --region ap-southeast-1 > workshop-aws-key.pem

# Set permissions (Linux/Mac only)
chmod 400 workshop-aws-key.pem
```

### 4. Development Tools

**Java Development Kit (JDK) 17:**
```bash
# Windows (chocolatey)
choco install openjdk17

# Linux (Ubuntu/Debian)
sudo apt-get install openjdk-17-jdk

# MacOS
brew install openjdk@17

# Verify
java -version
```

**Maven:**
```bash
# Windows
choco install maven

# Linux
sudo apt-get install maven

# MacOS
brew install maven

# Verify
mvn -version
```

**Node.js and npm:**
```bash
# Windows
choco install nodejs

# Linux
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# MacOS
brew install node

# Verify
node --version
npm --version
```

## Prepare Project Files

### 1. Clone or Download Project

```bash
# If you have Git repository
git clone <your-repo-url>
cd aws_project

# Or download and extract ZIP file
```

### 2. Project Structure

```
aws_project/
├── aws/
│   ├── infrastructure.yaml      # Main CloudFormation template
│   ├── cicd-pipeline.yaml       # CI/CD pipeline (optional)
│   ├── parameters.json          # Stack parameters
│   ├── deploy.bat              # Deploy script (Windows)
│   ├── deploy.sh               # Deploy script (Linux/Mac)
│   └── README.md               # Detailed instructions
├── BE/
│   └── workshop_BE/
│       ├── src/                # Backend source code
│       ├── pom.xml             # Maven configuration
│       └── README.md
└── FE/
    ├── src/                    # Frontend source code
    ├── package.json            # npm dependencies
    └── README.md
```

### 3. Configure Parameters

Open `aws/parameters.json` and update values:

```json
[
  {
    "ParameterKey": "ProjectName",
    "ParameterValue": "workshop-aws"
  },
  {
    "ParameterKey": "Environment",
    "ParameterValue": "dev"
  },
  {
    "ParameterKey": "KeyPairName",
    "ParameterValue": "workshop-aws-key"  // ⚠️ Replace with your key pair name
  },
  {
    "ParameterKey": "DBPassword",
    "ParameterValue": "YourStrongPassword123!"  // ⚠️ Use a strong password
  },
  {
    "ParameterKey": "InstanceType",
    "ParameterValue": "t3.micro"
  },
  {
    "ParameterKey": "DBInstanceClass",
    "ParameterValue": "db.t3.micro"
  }
]
```

**Important notes:**
- `KeyPairName`: Must match your created key pair name
- `DBPassword`: Minimum 8 characters with uppercase, lowercase, numbers, and special characters
- Don't commit this file with real passwords to Git

### 4. Update AMI ID

The CloudFormation template uses a default AMI ID. Update it for your region:

**Find AMI ID:**
```bash
# Find Amazon Linux 2023 AMI for ap-southeast-1
aws ec2 describe-images \
  --owners amazon \
  --filters "Name=name,Values=al2023-ami-*-x86_64" \
  --query 'Images | sort_by(@, &CreationDate) | [-1].[ImageId,Name,CreationDate]' \
  --region ap-southeast-1 \
  --output table
```

**Update in `infrastructure.yaml`:**

Find line ~530:
```yaml
LaunchTemplate:
  Properties:
    LaunchTemplateData:
      ImageId: ami-0c55b159cbfafe1f0  # ⚠️ Replace with your AMI ID
```

## Preparation Checklist

Ensure you have completed all the following steps:

- [ ] AWS account configured
- [ ] AWS CLI installed and configured (`aws configure`)
- [ ] EC2 Key Pair created
- [ ] Java 17 installed
- [ ] Maven installed
- [ ] Node.js and npm installed
- [ ] Project files downloaded
- [ ] `parameters.json` file updated
- [ ] AMI ID updated in `infrastructure.yaml`

### Validate AWS Credentials

```bash
# Check AWS credentials
aws sts get-caller-identity

# Expected output:
# {
#     "UserId": "AIDAXXXXXXXXXXXXXXXXX",
#     "Account": "123456789012",
#     "Arn": "arn:aws:iam::123456789012:user/your-username"
# }
```

### Validate CloudFormation Template

```bash
cd aws
aws cloudformation validate-template \
  --template-body file://infrastructure.yaml \
  --region ap-southeast-1
```

If successful, you'll see output with template parameters and outputs information.

## Cost Estimation

Before deployment, understand the costs:

| Service | Instance Type | Cost/month (USD) |
|---------|---------------|------------------|
| EC2 | t3.nano | $3.50 |
| RDS MySQL | db.t3.micro | $2.80 |
| API Gateway | - | $0.50 |
| S3 + CloudFront | - | $0.80 |
| Route 53 | - | $0.50 |
| Cognito | - | $0.10 |
| CloudWatch | - | $0.30 |
| CI/CD (CodePipeline) | - | $0.40 |
| **Total** | | **$8.90** |

**For workshop (2-3 hours):** ~$0.50-1.00

**Note:** 
- Costs apply to ap-southeast-1 region
- Use AWS Free Tier if account is eligible
- NAT Gateway (~$32/month) can be disabled to save costs

## Next Steps

After completing all preparation steps, you're ready to:

➡️ [Deploy Infrastructure with CloudFormation](../5.3-deploy-infrastructure/)

