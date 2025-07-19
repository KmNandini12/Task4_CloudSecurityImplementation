# Task4_CloudSecurityImplementation

**Company**: CODTECH IT SOLUTIONS

**Name**: Kumari Nandini

**Intern ID**: CT08DL671

**Domain**: Cloud Computing

**Mentor**: NEELA SANTOSH 

**Duration**: 8 Weeks

# Cloud Computing Internship – Task 4  
## IMPLEMENT IAM POLICIES, SECURE STORAGE, AND DATA ENCRYPTION ON A CLOUD PLATFORM.


---

## Objective

The objective of Task 4 is to implement a secure cloud storage system using **Amazon S3**, ensuring that access is tightly controlled using **IAM policies** and that data is **encrypted at rest**. The task focuses on applying best security practices in a cloud environment, including permission isolation, encryption, and verification through IAM user-based access.

---

## Tools and Technologies Used

- **Amazon S3** (Simple Storage Service): Scalable cloud storage used to store files.
- **IAM (Identity and Access Management)**: To securely manage access to AWS services.
- **AWS Root Account**: Used for full control and configuration.
- **IAM User Account**: Used for testing restricted access.
- **Server-Side Encryption (SSE-S3)**: To encrypt stored data automatically.
- **Bucket Policies**: JSON-based policies to control permissions at the bucket level.
- **Cloud Console and AWS Management Console**: Used for all administrative actions.

---

## Implementation Process

### 1. S3 Bucket Setup from Root Account

- Logged in to the AWS root account.
- Created a new S3 bucket named: `secure-storage-codetech`.
- Configured bucket settings:
  - **Public Access**: Disabled all block public access settings (to allow controlled access via policies).
  - **Versioning**: Enabled to retain versions of all uploaded files.
  - **Encryption**: Enabled **SSE-S3** (AES-256), which automatically encrypts objects upon upload.
  - **Bucket Key**: Kept **disabled** to avoid key-level overrides.

---

### 2. IAM Policy Configuration

- Created a custom IAM policy named `SecureS3-USER` with the following permissions:
  - `s3:ListBucket` – to allow listing of the bucket contents.
  - `s3:GetObject` – to allow reading (downloading) of individual objects.
  - `s3:PutObject` – to allow writing (uploading) of new objects.

- Policy was scoped specifically to:
  - `arn:aws:s3:::secure-storage-codetech` (bucket itself)
  - `arn:aws:s3:::secure-storage-codetech/*` (objects inside the bucket)

- Attached the policy to the existing IAM user `nandiniemp`.

- Policy saved as a file: **`secure-s3-access-policy.json`**

---

### 3. Access Testing using IAM User

- Signed in using the IAM user account.
- Verified access through the AWS Management Console:
  - **Successfully listed** the contents of the S3 bucket.
  - **Uploaded new objects** into the bucket.
  - **Downloaded and accessed** previously uploaded files.
- Attempted to open file URL directly:
  - Initially resulted in **Access Denied**.
  - Fixed by updating the bucket policy to allow public `s3:GetObject` access to that specific object path.

---

## Problems Faced and Resolutions

**&#8728; `Access Denied when listing bucket`** (IAM user couldn’t see objects in the bucket):   

--> Added `s3:ListBucket` permission to the policy.

                                                                                         
**&#8728; `Object not accessible via URL`** (Even after upload, public access was denied):       

--> Added `s3:GetObject` permission to object-level ARN in bucket policy.

                                                                                         
**&#8728; `Over-restrictive bucket policy`** (Combined IAM and bucket policy blocked access):    

--> Carefully tuned policy to allow only secure access with encryption enabled.

                                                                                         
**&#8728; `Credential Confusion`** (Accidentally tried using root credentials in testing script):

--> Used IAM user credentials as per best practices. 

---

## Files and Repository Contents

`secure-s3-access-policy.json`   - IAM policy JSON document created for S3 access. 

`bucket-settings.png`            - Screenshot showing bucket configuration (access, versioning, encryption). 

`encryption-settings.png`        - SSE-S3 encryption configuration.

`iam-policy-editor.png`          - IAM custom policy configuration interface. 

`access-confirmation.png`        - IAM user testing access to the bucket. 

---

## Security Best Practices Followed

- **Principle of Least Privilege (PoLP)**: IAM user was given only the required permissions to interact with the bucket.
- **Encryption at Rest**: All data uploaded to the bucket was automatically encrypted using server-side encryption.
- **No Public Access to Bucket**: Public access was restricted entirely except for controlled object-level testing.
- **Use of IAM User Instead of Root**: The root account was used only for setup. All access operations were validated using an IAM user.

---

## Conclusion

This task successfully demonstrated the creation and configuration of a **secure cloud storage environment** using AWS S3. It involved working with **IAM users**, **custom policies**, **bucket encryption**, and **access control verification**. All configurations followed AWS security best practices and provided hands-on experience in cloud security management.

---
