## GitHub Deployments Manager — One‑click experience

This package wraps Port's "Visualize and manage GitHub deployments" guide into a ready‑to‑use experience. It provides:

- Blueprints for GitHub workflows and workflow runs
- Actions to trigger, rerun, and cancel workflow runs
- A GitHub integration mapping to sync repository, workflow, and workflow run data
- A dashboard widget to visualize and track deployments

References:

- Guide: [Visualize and manage GitHub deployments](https://docs.port.io/guides/all/visualize-and-manage-github-deployments/)
- PyPI: [`port-experience`](https://pypi.org/project/port-experience/)

### What's included

- `setup/*`: All actions, blueprints, mappings, and widgets that will be created by the `port-experience`
- `.env.sample`: This contains environment variables you need to set

### Prerequisites

- A Port account and credentials
- A GitHub account with access to repositories you want to manage
- GitHub integration configured in Port (or GitHub token for API access)

### Required environment variables

Create a `.env` file at the repository root. You can start from `gh_deployments_manager/.env.sample`:

The actions use GitHub API endpoints and require a GitHub token. Configure the following:

- `_GITHUB_TOKEN`: Your GitHub personal access token or GitHub App token with appropriate permissions
- `WORKFLOW_REPO`: The GitHub repository where workflows are located (format: `org/repo` or `user/repo`)

### Actions included

This experience includes three self-service actions:

1. **Trigger Workflow Run**: Triggers a GitHub workflow run in the specified repository with environment selection (test, staging, production)
2. **Rerun Workflow Run**: Reruns a failed or completed workflow run
3. **Cancel Workflow Run**: Cancels an in-progress workflow run

### Blueprints included

- **githubWorkflow**: Represents a GitHub Actions workflow with properties like path, status, and timestamps
- **githubWorkflowRun**: Represents a workflow run execution with properties like status, conclusion, run number, and deployment information

### Integration mapping

The GitHub integration mapping syncs:

- **Repositories** → `service` blueprint entities
- **Workflows** → `githubWorkflow` blueprint entities
- **Workflow Runs** → `githubWorkflowRun` blueprint entities

The mapping automatically creates relationships between workflows and their repositories, and between workflow runs and their parent workflows.

### Dashboard widget

The included dashboard provides:

- Total deployments count (filtered for deployment-related workflows)
- Deployments by status (pie chart)
- Quick action to trigger workflow runs
- Table view of all deployments with filtering

### Commands and how to run

Prerequisites: Python 3.10+.

Install the experience package:

```bash
pip install --upgrade port-experience
```

Run the experience:

```bash
# if running from gh_deployments_manager directory
experience apply

# if running from experience-marketplace directory
experience apply --gh_deployments_manager
```
