# Portfolio Website – AWS S3 + CloudFront + CI/CD

A simple personal portfolio website built with HTML/CSS and hosted on **AWS S3** with a **CloudFront CDN** in front.  
Code changes are automatically deployed from **GitHub → AWS** using **CodePipeline** and **CodeBuild**.

---

## 🚀 Features

- Static portfolio website (HTML/CSS)
- Hosted on **Amazon S3** (static website hosting)
- Distributed via **Amazon CloudFront** (global CDN)
- **CI/CD pipeline**:
  - Source: GitHub
  - Build & deploy: AWS CodeBuild
  - Orchestrator: AWS CodePipeline
- Automatic **CloudFront cache invalidation** on every deploy

---

## 🧱 Tech Stack

**Frontend**

- HTML
- CSS
- JS

**AWS & DevOps**

- Amazon S3 – static website hosting
- Amazon CloudFront – CDN + HTTPS
- AWS CodePipeline – CI/CD orchestration
- AWS CodeBuild – runs `buildspec.yml` and deploys to S3
- IAM – roles & permissions for CodeBuild and CodePipeline
- Git & GitHub – version control

---

## 🏗 Architecture Overview

1. Code is pushed to **GitHub** (`main` branch).
2. **AWS CodePipeline** detects the change.
3. **CodeBuild** runs using `buildspec.yml`:
   - Syncs repo files to the S3 bucket
   - Invalidates the CloudFront cache
4. Users access the site via the **CloudFront URL**.

---

## 🔁 CI/CD Details

`buildspec.yml` (simplified):

```yaml
version: 0.2

phases:
  build:
    commands:
      - aws s3 sync . s3://adi-portfolio-web --delete --exclude ".git/*" --exclude "buildspec.yml"
      - aws cloudfront create-invalidation --distribution-id E1C4JGIRSODAXQ --paths "/*"
