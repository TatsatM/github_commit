# .github/workflows/commit.yml
name: Daily Commit

on:
  schedule:
    - cron: '0 10 * * *'  # Runs daily at 9 AM UTC
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Make a tiny commit
        run: |
          echo "$(date)" >> activity.log
          git config --global user.name "Your Name"
          git config --global user.email "your-email@example.com"
          git add activity.log
          git commit -m "daily contribution $(date)"
          git push
