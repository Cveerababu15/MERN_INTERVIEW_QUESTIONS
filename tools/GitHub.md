# GitHub Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** GitHub fundamentals + collaboration workflow
> **Goal:** Understand how Git repositories are hosted and how teams collaborate.

---

# 1. What is GitHub?

GitHub is a platform for hosting Git repositories and collaborating on software projects.

It provides features such as:

```text
Repositories
Branches
Pull Requests
Issues
Code Reviews
Actions
Releases
Project Management
```

Simple difference:

```text
Git
→ Version control system

GitHub
→ Platform for hosting and collaborating around Git repositories
```

---

# 2. Git vs GitHub

| Git                    | GitHub                         |
| ---------------------- | ------------------------------ |
| Version control system | Hosting/collaboration platform |
| Runs locally           | Web/cloud service              |
| Tracks code history    | Hosts repositories             |
| Branches and commits   | Pull requests and code reviews |
| Works without GitHub   | Commonly uses Git underneath   |

---

# 3. What is a GitHub repository?

A GitHub repository is a remotely hosted Git repository.

It can contain:

```text
Source code
README
Documentation
Issues
Branches
Commit history
Pull Requests
```

Example:

```text
GitHub
  ↓
MERN_INTERVIEW_QUESTIONS
  ↓
frontend/
backend/
database/
api/
tools/
```

---

# 4. What is a remote repository?

A remote repository is a repository stored somewhere outside your local machine.

Example:

```text
Local Repository
      ↕
GitHub Repository
```

Common remote name:

```text
origin
```

Check it:

```bash
git remote -v
```

---

# 5. How do you connect a local Git repository to GitHub?

Create a repository on GitHub, then:

```bash
git remote add origin https://github.com/username/project.git
```

Verify:

```bash
git remote -v
```

Push:

```bash
git push -u origin main
```

---

# 6. What is a README?

`README.md` explains a repository.

It can contain:

```text
Project description
Features
Tech stack
Installation
Usage
Folder structure
API information
Screenshots
Author information
```

A good README helps someone understand the project quickly.

---

# 7. What is a GitHub branch?

A branch allows independent development.

Example:

```text
main
 │
 ├── feature/authentication
 ├── feature/orders
 └── feature/profile
```

Developers can work on features without directly changing the main branch.

---

# 8. What is a Pull Request?

A Pull Request, commonly called a PR, is a request to merge changes from one branch into another.

Typical flow:

```text
Create Branch
      ↓
Write Code
      ↓
Commit
      ↓
Push Branch
      ↓
Create Pull Request
      ↓
Code Review
      ↓
Changes if required
      ↓
Merge
```

---

# 9. Why are Pull Requests useful?

Pull Requests support:

```text
Code review
Discussion
Testing
Collaboration
Quality control
Change tracking
```

They allow team members to review code before it is merged.

---

# 10. What is code review?

Code review is the process of examining code changes before they are merged.

Reviewers may check:

```text
Correctness
Code quality
Security
Performance
Naming
Architecture
Tests
```

---

# 11. What is a GitHub Issue?

An Issue is used to track work, bugs, questions, or improvements.

Example:

```text
Issue #25
Title:
Fix login validation error
```

It can contain:

```text
Description
Labels
Assignee
Comments
References
```

---

# 12. What are GitHub labels?

Labels categorise issues and Pull Requests.

Examples:

```text
bug
feature
documentation
enhancement
help wanted
good first issue
```

They help teams organise work.

---

# 13. What is a GitHub fork?

A fork is a copy of another GitHub repository under your own GitHub account.

Common workflow:

```text
Original Repository
        ↓
      Fork
        ↓
Your GitHub Account
        ↓
Clone
        ↓
Make Changes
        ↓
Pull Request
```

Forks are commonly used when you do not have direct write access to the original repository.

---

# 14. What is a GitHub organization?

A GitHub organization is a shared GitHub account structure for teams or companies.

It can contain multiple repositories and manage:

```text
Members
Teams
Permissions
Repositories
```

---

# 15. What are GitHub permissions?

Permissions control what users can do with repositories.

Examples include abilities related to:

```text
Read
Write
Maintain
Admin
```

Exact permissions depend on repository and organization settings.

---

# 16. What is a GitHub Actions?

GitHub Actions is a CI/CD automation platform integrated with GitHub.

It can automatically:

```text
Run tests
Run linting
Build applications
Deploy applications
Run scripts
```

Example workflow:

```text
Push Code
   ↓
GitHub Actions
   ↓
Install Dependencies
   ↓
Run Tests
   ↓
Build
   ↓
Deploy
```

---

# 17. What is CI/CD?

CI/CD stands for:

```text
Continuous Integration
Continuous Delivery / Deployment
```

### Continuous Integration

Automatically build and test code changes.

### Continuous Delivery/Deployment

Automate the process of preparing or deploying changes.

Example:

```text
Developer Push
      ↓
CI
      ↓
Tests
      ↓
Build
      ↓
Deployment
```

---

# 18. What is a GitHub Release?

A release is a published version of a project.

Example:

```text
v1.0.0
v1.1.0
v2.0.0
```

Releases can include:

```text
Version information
Release notes
Tags
Build artifacts
```

---

# 19. What is a Git tag?

A tag is a named reference to a specific Git commit.

Example:

```bash
git tag v1.0.0
```

Push:

```bash
git push origin v1.0.0
```

Tags are commonly used to identify releases.

---

# 20. What is a protected branch?

A protected branch has rules that restrict certain operations.

For example, a team may require:

```text
Pull Request
Code review
Passing CI checks
```

before merging into `main`.

This helps protect important branches.

---

# 21. What is a GitHub Personal Access Token?

A Personal Access Token (PAT) can be used to authenticate Git operations and API access when supported instead of using a password.

Treat tokens like passwords.

Never commit them into:

```text
Source code
.env files
README
Git repository
```

---

# 22. What should never be pushed to GitHub?

Do not commit secrets such as:

```text
.env
API keys
Database passwords
JWT secrets
Private credentials
Access tokens
```

Use:

```gitignore
.env
```

and configure secrets securely in your deployment/CI environment.

---

# 23. How do you clone a GitHub repository?

```bash
git clone https://github.com/username/project.git
```

Then:

```bash
cd project
```

Install dependencies if it is a Node project:

```bash
npm install
```

---

# 24. What is the typical team GitHub workflow?

```text
GitHub Repository
       ↓
Create Feature Branch
       ↓
Write Code
       ↓
git add
       ↓
git commit
       ↓
git push
       ↓
Create Pull Request
       ↓
Code Review
       ↓
CI Checks
       ↓
Merge
       ↓
main
```

---

# 25. How should a fresher use GitHub professionally?

A useful GitHub profile should show:

```text
Good repositories
Clean README files
Meaningful commit messages
Working projects
Relevant technologies
Consistent project structure
Useful documentation
```

For a MERN developer, repositories can demonstrate:

```text
React
Node.js
Express
MongoDB
TypeScript
REST APIs
Authentication
Testing
Deployment
```

---

# GitHub Revision Checklist

* [ ] GitHub
* [ ] Git vs GitHub
* [ ] Repository
* [ ] Remote repository
* [ ] README
* [ ] Branches
* [ ] Pull Requests
* [ ] Code review
* [ ] Issues
* [ ] Labels
* [ ] Fork
* [ ] Organizations
* [ ] Permissions
* [ ] GitHub Actions
* [ ] CI/CD
* [ ] Releases
* [ ] Tags
* [ ] Protected branches
* [ ] Personal Access Tokens
* [ ] Repository security
* [ ] Team workflow

---

# Final Git + GitHub Workflow

```text
                 LOCAL
                   │
             Write Code
                   ↓
              git status
                   ↓
               git add
                   ↓
              git commit
                   ↓
              git push
                   ↓
                GITHUB
                   │
             Pull Request
                   ↓
              Code Review
                   ↓
             CI / Testing
                   ↓
                Merge
                   ↓
                 main
                   ↓
               Deploy
```

### One-Line Interview Answer

> **Git manages version history locally, while GitHub provides a remote platform for hosting Git repositories and collaborating through Pull Requests, Issues, reviews, and automation.**
