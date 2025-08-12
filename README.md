# Phishing-website-detection
name: Update OpenPhish Blacklist

on:
  schedule:
    - cron: '0 2 * * *'  # 每天凌晨 2 點 UTC 執行
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - run: pip install requests
      - run: python update_blacklist.py
      - run: git config --global user.name "github-actions"
      - run: git config --global user.email "actions@github.com"
      - run: git add urls.json
      - run: git commit -m "Update blacklist"
      - run: git push
