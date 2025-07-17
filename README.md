# CloudFormation S3 Bucket Deployment via CodePipeline

## Files
- `s3-bucket-template.yaml`: CloudFormation template for creating an S3 bucket with versioning support.

## How to Use

### 1. Validate the Template
```bash
aws cloudformation validate-template --template-body file://s3-bucket-template.yaml
```

### 2. Push to GitHub
Create a new GitHub repo and push the file:
```bash
git init
git remote add origin https://github.com/YOUR_USERNAME/cf-s3-bucket-deployment.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

### 3. Create AWS CodePipeline
- Source: GitHub (connect your repo)
- Deploy: AWS CloudFormation
  - Stack name: `MyS3BucketStack`
  - Template: `s3-bucket-template.yaml`
  - Parameters:
    - BucketName: `your-unique-s3-bucket-name`
    - VersioningStatus: `Enabled` or `Suspended`

### 4. Test Automatic Deployment
- Edit the YAML (e.g., add tags)
- Commit and push the change to GitHub
- Confirm the pipeline triggers automatically

### 5. Verify & Cleanup
- Check S3 bucket in AWS Console
- Cleanup using:
```bash
aws cloudformation delete-stack --stack-name MyS3BucketStack
```
