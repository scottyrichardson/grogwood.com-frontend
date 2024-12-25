# Grogwood.com Frontend

This project uses NodeJS and gulp to build a deployable artifact located in `dist`. The artifact gets deployed to an AWS S3 bucket that sits behind a CloudFront distribution.

**Build and deployment is handled automatically by CI/CD actions in this repo**. The process to manually deploy is detailed below.

## Prerequisites

- Node.js
- AWS CLI (for deployment)

## NodeJS

Install required packages:

```bash
# Install Gulp
npm install -g gulp npm-check-updates

# Install project dependencies:
npm install
```

### Building the Project

```bash
gulp
# or
gulp prod
```

### Updating Dependencies

Check and update dependencies:

```bash
# Update package.json versions
ncu -u

# Install updated packages
npm install
```

## AWS

### CLI

1. Create access key in AWS Portal:

   - Login to AWS Portal
   - Navigate to profile → Security Credentials
   - Create new access key under "Access Keys" section

2. Configure AWS CLI with access key:

```bash
aws configure
```

### S3 Bucket

Upload `dist` to an S3 bucket:

```bash
aws s3 sync dist/ s3://<s3-bucket-name>
```

### CloudFront

Invalidate CloudFront cache:

```bash
aws cloudfront create-invalidation --distribution-id <distribution-id> --paths "/*"
```
