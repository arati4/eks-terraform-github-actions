# 🧠 **What is GitHub Actions?**


👉 **GitHub Actions** is an **automation platform** built directly into **GitHub** that helps you:

* **Build**, **test**, and **deploy** your code automatically.
* Create **CI/CD pipelines** without needing external tools like Jenkins or CircleCI.

💡 In simple words:

> Whenever you push code, create a pull request, or tag a release — GitHub Actions can automatically do tasks like testing, packaging, or deploying your app 🚀.

git status

---

# 🌟 **Benefits of GitHub Actions**

| 💥 Benefit                       | 📘 Description                                                                                           |
| -------------------------------- | -------------------------------------------------------------------------------------------------------- |
| ⚙️ **Built into GitHub**         | No need to install or manage separate CI/CD servers — works right in your repo.                          |
| ⏱️ **Faster Setup**              | Just create a `.yml` file inside `.github/workflows/`.                                                   |
| 🧩 **Reusable Actions**          | Use 10,000+ prebuilt actions from the [GitHub Marketplace](https://github.com/marketplace?type=actions). |
| ☁️ **Hosted Runners**            | GitHub provides free Linux, Windows, and macOS runners.                                                  |
| 🔒 **Secure Secrets Management** | Store tokens, keys, and passwords in GitHub Secrets safely.                                              |
| 🔄 **Parallel & Matrix Builds**  | Test your code on multiple OS or versions simultaneously.                                                |
| 📦 **Integration Ready**         | Works seamlessly with AWS, Azure, Docker, Slack, Kubernetes, etc.                                        |
| 💰 **Free for Public Repos**     | You get free minutes for open-source projects. 


                                                          |

---

# ⚙️ **GitHub Actions Workflow (in Detail)**

GitHub Actions uses **Workflows**, defined in YAML, to describe automation pipelines.

---

### 🧩 **1️⃣ Workflow File**

* A **workflow** is a `.yml` file inside:
  `.github/workflows/your-workflow.yml`

---

### 🔔 **2️⃣ Trigger (Event)**

Defines **when** the workflow should run.
Examples:

```yaml
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```

🟢 Triggered when code is pushed or a PR is opened against `main`.

---

### 🧱 **3️⃣ Jobs**

A **job** is a set of steps that run on the same runner (VM).
Example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

💡 You can have multiple jobs like `build`, `test`, `deploy`.

---

### ⚙️ **4️⃣ Steps**

Each **step** is a command or an action that runs inside a job.
Example:

```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v4

  - name: Set up Node.js
    uses: actions/setup-node@v4
    with:
      node-version: 18

  - name: Install dependencies
    run: npm install

  - name: Run tests
    run: npm test
```

---

### 🧰 **5️⃣ Actions**

An **action** is a prebuilt piece of automation code you can reuse.
For example:

* `actions/checkout` → checks out code
* `actions/setup-node` → installs Node.js

You can find thousands on the GitHub Marketplace.

---

# 🆚 **Jenkins vs GitHub Actions**

| Feature               | 🧩 **Jenkins**                       | 🚀 **GitHub Actions**                                |
| --------------------- | ------------------------------------ | ---------------------------------------------------- |
| 🏗️ Setup             | Manual installation on your server   | No setup — built into GitHub                         |
| ☁️ Hosting            | Self-hosted                          | GitHub-hosted or self-hosted                         |
| 🧾 Configuration      | Jenkinsfile (Groovy)                 | YAML workflows                                       |
| 🔧 Plugins            | Thousands (manual management)        | GitHub Marketplace actions                           |
| 🔒 Security           | Must manage access, secrets, plugins | GitHub manages secrets securely                      |
| 💰 Cost               | Free but requires infrastructure     | Free for public repos; paid for private after limits |
| 🧑‍💻 User Experience | Complex (Jenkins UI)                 | Simple, integrated in GitHub UI                      |
| 🚀 Integration        | Requires webhooks                    | Native GitHub integration                            |
| 🧩 Scalability        | Needs Jenkins agents                 | Auto-scaled GitHub runners                           |
| 🔄 Maintenance        | Requires DevOps to maintain servers  | Fully managed by GitHub                              |

**✅ Verdict:**
If your project is already on GitHub, **GitHub Actions** is easier, faster, and integrated natively.
If you need **highly complex enterprise pipelines**, **Jenkins** is still powerful and customizable.

---

# 🧾 **Example: Detailed GitHub Actions YAML File**

Here’s a **complete CI/CD workflow** example for a Node.js application:

```yaml
name: Node.js CI/CD Pipeline 🚀

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch: # Manual trigger

jobs:
  build:
    name: 🧱 Build and Test
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository 🧾
        uses: actions/checkout@v4

      - name: Setup Node.js 🧩
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install dependencies 📦
        run: npm install

      - name: Run tests ✅
        run: npm test

      - name: Build project 🏗️
        run: npm run build

  deploy:
    name: 🚀 Deploy to AWS
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Configure AWS credentials 🔐
        uses: aws-actions/configure-aws-credentials@v3
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-south-1

      - name: Deploy to S3 bucket ☁️
        run: |
          aws s3 sync ./build s3://my-app-bucket --delete

      - name: Invalidate CloudFront cache ⚡
        run: |
          aws cloudfront create-invalidation \
            --distribution-id ABCDEFGHIJ \
            --paths "/*"
```
---
