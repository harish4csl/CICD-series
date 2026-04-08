# 📘 GitHub Actions + Terraform Pipeline

## 🚀 What is GitHub Actions?

GitHub Actions is a CI/CD tool provided by GitHub.

It helps to:
- Automate workflows  
- Build, test, and deploy code  
- Run pipelines directly from your repository  

---

## 🔄 What is a Pipeline?

A pipeline is a sequence of automated steps:

1. Fetch code  
2. Build or validate  
3. Test  
4. Deploy  

👉 In GitHub Actions, pipelines are called **workflows**

---

## 📂 Terraform Workflow

```yaml
name: Terraform Deploy

on:
  workflow_dispatch:

jobs:
  terraform:
    runs-on: ubuntu-latest

    env:
      AWS_ACCESS_KEY_ID: \${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: \${{ secrets.AWS_SECRET_ACCESS_KEY }}
      AWS_DEFAULT_REGION: us-east-1

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3

      - name: Terraform Init
        run: terraform init

      - name: Terraform Validate
        run: terraform validate

      - name: Terraform Plan
        run: terraform plan -out=tfplan

      - name: Terraform Apply
        run: terraform apply -auto-approve tfplan
