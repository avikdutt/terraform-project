# 🚀 GitLab CI/CD Pipeline for Terraform on AWS

This project automates Terraform deployments using GitLab CI/CD pipelines. It provisions AWS resources using Terraform with stages for initialization, validation, planning, applying, and destroying infrastructure.

## 🔧 Tech Stack

- **Terraform** v1.8.3
- **AWS Provider** v5.10.0
- **GitLab CI/CD** with SaaS Runners
- **Docker** (Terraform image: `hashicorp/terraform:light`)
- **Alpine** for base container setup

---

## 📁 Project Structure

├── .gitlab-ci.yml # GitLab CI pipeline definition
├── main.tf # Terraform configuration (e.g., AWS S3 bucket)
└── README.md # Project overview and usage


---

## 🚀 Pipeline Stages

| Stage    | Description                                |
|----------|--------------------------------------------|
| init     | Initializes Terraform working directory     |
| validate | Validates Terraform configuration syntax    |
| plan     | Creates and stores the execution plan       |
| apply    | Applies the Terraform changes (manual)      |
| destroy  | Destroys the provisioned resources (manual) |

---

## 🔐 AWS Resource Provisioned

- An **S3 bucket** is created using the `aws_s3_bucket` resource.
- Bucket name is passed using CI/CD environment variable `TF_VAR_bucketname`.

---

## 🔄 How It Works

1. GitLab runner pulls the Terraform Docker image.
2. Each job runs Terraform commands in a stateless container.
3. Terraform plugin cache is handled dynamically in SaaS runner setup.
4. Manual approval is required for `apply` and `destroy` stages.

---

## ✅ Prerequisites

- AWS credentials are configured via GitLab CI/CD variables:
  - `AWS_ACCESS_KEY_ID`
  - `AWS_SECRET_ACCESS_KEY`
- Ensure `TF_VAR_bucketname` is set for dynamic bucket naming.

---

## 💡 Sample Terraform Output

```bash
Terraform will perform the following actions:

  # aws_s3_bucket.mybucket will be created
  + resource "aws_s3_bucket" "mybucket" {
      bucket = "avik-tf-s3bucket-2025"
      ...
    }

Plan: 1 to add, 0 to change, 0 to destroy.
