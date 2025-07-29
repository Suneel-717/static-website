# 🚀 Static Website CI/CD Deployment to AWS S3

This project sets up a **CI/CD pipeline** using **GitHub Actions** to automatically deploy a static website to **AWS S3**.

## 🌐 Live Website
> [https://your-domain-or-s3-url](https://your-domain-or-s3-url)

---

## 🧰 Tech Stack

- HTML/CSS (Static Website)
- AWS S3 (Static Hosting)
- GitHub Actions (CI/CD)
- Bash/YAML scripting

---

## 📦 Folder Structure

├── index.html
├── styles.css
├── .github/
│ └── workflows/
│ └── deploy.yml
├── README.md
└── .gitignore

---

## 🔄 CI/CD Workflow

### Trigger:
- Every push to `main` branch

### Actions:
1. Checkout code
2. Configure AWS credentials
3. Sync files to S3 bucket

```yaml
# File: .github/workflows/deploy.yml
name: Deploy Static Website to S3

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Deploy to S3
        run: |
          aws s3 sync . s3://${{ secrets.S3_BUCKET_NAME }} --delete

| Secret Name             | Description           |
| ----------------------- | --------------------- |
| `AWS_ACCESS_KEY_ID`     | IAM user's access key |
| `AWS_SECRET_ACCESS_KEY` | IAM user's secret key |
| `AWS_REGION`            | e.g. `us-east-1`      |
| `S3_BUCKET_NAME`        | Your S3 bucket name   |

