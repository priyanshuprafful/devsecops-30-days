# Day 00 - Repository Setup

## What I learned (in my own words)
1. Created two repositories with separate purposes: `devsecops-30-days` for the daily learning log and `pulsewatch` for the project code.
2. Both repositories are public with a README and a Python `.gitignore`. This is a personal learning project on my own AWS account, so there is no employer or client data involved.
3. Public repositories are scanned by bots looking for leaked credentials, so I will never commit secrets, keys or state files.

## Commands I ran
None. All steps were done in the GitHub web interface.

## What broke and how I fixed it
Nothing broke today.

## Interview questions

### 1. Why keep a learning log and a project in separate repositories?
The learning log changes every day and is messy by nature: notes, failed experiments, half-finished labs. The project repository should show a clean history, a clear README and a structure a reviewer can follow in minutes. Separating them also lets the project grow its own CI/CD, branch protection and releases without noise from daily notes, and lets me change visibility or access for one without affecting the other.

### 2. How do you prevent secrets from being committed to Git?
I use several layers:
- Never hardcode secrets. Read them from environment variables or a secrets manager (AWS Secrets Manager or SSM Parameter Store).
- Keep `.env`, `*.pem` and `*.tfstate` in `.gitignore`.
- Run a pre-commit hook such as gitleaks to block commits that contain secrets.
- Enable GitHub secret scanning and push protection.
- Run a secret scan in CI as a backstop.
If a secret does leak, I revoke and rotate it immediately. Deleting the commit is not enough, because the secret remains in history, forks and clones.

### 3. When would you choose a public repository over a private one?
Public suits open-source work, portfolios and learning projects that contain no sensitive data, because visibility helps with feedback and credibility. Private suits proprietary code, client work, infrastructure details and anything pre-release. The trade-off is exposure: public code is read by everyone, including bots, so it needs strict secret hygiene. My repositories are public because they are personal learning work with no sensitive data.

## Tomorrow
1. Set up AWS account safety: root MFA, budget alert(optional), IAM user.
2. Launch a RHEL EC2 instance as my cloud workstation and connect over SSH.
