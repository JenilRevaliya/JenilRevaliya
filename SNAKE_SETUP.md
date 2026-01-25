# GitHub Profile Snake Animation Setup

This workflow file will generate the contribution snake animation for your GitHub profile.

## Setup Instructions:

1. **Create the workflow directory** (if it doesn't exist):
   ```bash
   mkdir -p .github/workflows
   ```

2. **Create this workflow file** at `.github/workflows/snake.yml`

3. **Enable GitHub Actions**:
   - Go to your GitHub profile repository settings
   - Navigate to Actions → General
   - Enable "Read and write permissions" for workflows

4. **The snake will auto-generate**:
   - Runs every 12 hours automatically
   - Also runs on every push to main branch
   - Generates both light and dark mode versions

## Workflow File Content:

```yaml
name: Generate Snake Animation

on:
  schedule:
    - cron: "0 */12 * * *" # Every 12 hours
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    
    steps:
      - name: Generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=ocean_blue
            
      - name: Push github-contribution-grid-snake.svg to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Custom Blue Theme:

The snake uses the `ocean_blue` palette which matches your website's blue theme:
- Primary: #0096c7
- Gradient: #00aaad  
- Accent: #22d3ee

Once set up, the snake will appear in your README automatically! 🐍✨
