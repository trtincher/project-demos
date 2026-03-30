# project-demos

Public demo pages for private project PRs. Hosted via GitHub Pages.

**Live site:** https://trtincher.github.io/project-demos/

## Structure

```
project-repos.json              # Maps folder names → GitHub repos
{project-name}/
  pr-{N}-{description}/
    index.html                  # Demo page with screenshots + video
    ss-*.png                    # Screenshots
    pr-demo-video.webm          # Recorded walkthrough
```

## Adding a new demo

1. Create a folder: `{project}/pr-{N}-{description}/`
2. Add screenshots, video, and `index.html`
3. Update root `index.html` with a link
4. Push to `main` — GitHub Pages deploys automatically

## Adding a new project

Add an entry to `project-repos.json`:
```json
{
  "dndapp": "trtincher/DNDApp",
  "myproject": "trtincher/MyProject"
}
```

## Auto-cleanup

A GitHub Actions workflow runs daily at 6am UTC. It:
1. Scans all `*/pr-*/` folders
2. Looks up the corresponding repo in `project-repos.json`
3. Checks if the PR is merged via the GitHub API
4. Deletes demos for merged PRs and updates `index.html`

You can also trigger cleanup manually: Actions tab > "Cleanup merged PR demos" > Run workflow.

### Setup

The cleanup workflow needs a `DEMO_CLEANUP_TOKEN` secret — a GitHub personal access token that can read PR status from your private repos.

1. Create a fine-grained token at https://github.com/settings/tokens with read access to your private repos
2. Add it as a secret in this repo: Settings > Secrets > Actions > `DEMO_CLEANUP_TOKEN`
