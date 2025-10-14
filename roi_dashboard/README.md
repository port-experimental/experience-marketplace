## Actions ROI dashboard — One‑click experience

This package wraps Port's "Create an actions ROI dashboard" guide into a ready‑to‑use experience. It provides:

- A self‑service action (`setup_new_action`) that scaffolds the ROI data model and wiring
- A template GitHub Actions workflow you can drop into your repository

References:

- Guide: [Create an actions ROI dashboard](https://docs.port.io/guides/all/create-roi-dashboard/)
- PyPI: [`port-experience` 0.1.0](https://pypi.org/project/port-experience/0.1.0/)

### What’s included

- `setup/*`: All actions, blueprints and widgets that will be created by the `port-experience`
- `your_github_setup`: This contains the GitHub workflow setup required to allow this to run
- `.env.sample`: This contains environment variables you need to set

Note: GitHub requires workflows to live at repo root under `your_github_setup`. We include the workflow here as a template so you can copy it to your repository root.

### Prerequisites

- A Port account and credentials
- A GitHub repository where the workflow will run
- GitHub Secrets configured in that repository

### Required GitHub secrets

Add these repository secrets in GitHub → Settings → Secrets and variables → Actions:

- `PORT_CLIENT_ID`: your Port client ID
- `PORT_CLIENT_SECRET`: your Port client secret
- `PORT_BASE_URL` (optional): Port API base URL, default is `https://api.getport.io`

If your organization uses a personal access token instead of client credentials, set:

- `PORT_API_TOKEN`: your Port API token

The workflow prefers `PORT_CLIENT_ID`/`PORT_CLIENT_SECRET`; if absent, it will fall back to `PORT_API_TOKEN`.

### Wiring the experience to your repo

The self‑service action uses a GitHub invocation and is configured to call a workflow named `create-port-automation.yml` in your repository. It reads the target repository from environment variables so you don’t need to edit JSON:

- `var__org`: `SET_UP_NEW_ACTION_ORG`
- `var__repo`: `SET_UP_NEW_ACTION_REPO`

Provide these by creating a `.env` at your repository root. You can start from `roi_dashboard/env.sample`:

```
SET_UP_NEW_ACTION_ORG=your-org-or-user
SET_UP_NEW_ACTION_REPO=your-repo
```

### Commands and how to run

Prerequisites: Python 3.10+.

Install the experience package:

```bash
pip install --upgrade port-experience==0.1.0
```

Run the experience:

```bash
port-experience-apply
```

