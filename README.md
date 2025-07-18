# 📦 AWS CloudFormation + CodePipeline: Automated S3 Bucket Deployment

## ✅ Objective
To automate the provisioning of an S3 bucket using AWS **CloudFormation** and **CodePipeline**, integrated with **GitHub** for CI/CD.

---

## 🗂️ Files Used

- `s3-bucket-template.yaml`: CloudFormation template to create an S3 bucket with versioning.
- GitHub Repo: [Lab3-cloudformation](https://github.com/KeerthanaGarimella/Lab3-cloudformation)

---

## 🛠️ Steps Performed

### 1️⃣ CloudFormation Template Creation

Created a YAML file with:
- Parameters: `BucketName`, `VersioningStatus`
- Resources: S3 bucket with configurable versioning

```yaml
Parameters:
  BucketName:
    Type: String
  VersioningStatus:
    Type: String
    AllowedValues:
      - Enabled
      - Suspended
    Default: Suspended

Resources:
  S3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Ref BucketName
      VersioningConfiguration:
        Status: !Ref VersioningStatus
```

✅ **Validation**:
```bash
aws cloudformation validate-template --template-body file://s3-bucket-template.yaml
```

---

### 2️⃣ GitHub Setup

- Initialized Git repository in `cf-s3-bucket-deployment` folder
- Committed the template
- Linked to GitHub repo: `https://github.com/KeerthanaGarimella/Lab3-cloudformation`
- Commands used:
```bash
git init
git add .
git commit -m "Initial CloudFormation template for S3 bucket"
git remote add origin https://github.com/KeerthanaGarimella/Lab3-cloudformation.git
git branch -M main
git push -u origin main
```

---

### 3️⃣ CodePipeline Configuration

- Created a pipeline: `Lab-3cloudformation`
- **Source**: GitHub repository (main branch)
- **Deploy**: AWS CloudFormation
  - Stack name: `s3-bucket-cft`
  - Template file: `s3-bucket-template.yaml`
  - Parameters used:
    - `BucketName = keerthi-s3-bucket-01`
    - `VersioningStatus = Enabled`

---

### 4️⃣ Automated Deployment

- Pushed a change to GitHub → CodePipeline triggered automatically
- Stack successfully created in CloudFormation
- Bucket verified in S3 Console

---

### 5️⃣ Verification

- ✅ S3 Bucket: `keerthi-s3-bucket-01` created and visible in S3 console
- ✅ Stack: `s3-bucket-cft` created with `CREATE_COMPLETE` status
- ✅ Pipeline: Both **Source** and **Deploy** stages succeeded

---

## 📸 Screenshots Provided

1. S3 Console with bucket `keerthi-s3-bucket-01`
2. CloudFormation Console showing `s3-bucket-cft` stack as CREATE_COMPLETE
3. CodePipeline Console showing successful Source and Deploy stages

---

## 🧹 Cleanup (Optional)

```bash
aws cloudformation delete-stack --stack-name s3-bucket-cft
```

---

## 📌 Summary

Successfully implemented a CI/CD pipeline that automatically provisions AWS infrastructure using CloudFormation triggered by GitHub commits. Validated the setup with successful deployments and resource creation.

