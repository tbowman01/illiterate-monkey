# illiterate-monkey
dynamic sast scan

```yaml
name: "SAST and CodeQL Analysis"

on:
  push:
    branches:
      - main
      - develop
  pull_request:
    branches:
      - main
      - develop
  workflow_dispatch:
  schedule:
    - cron: "0 8 * * 0" # Weekly schedule

jobs:
  analyze:
    name: "Static Application Security Testing (SAST)"
    runs-on: ubuntu-latest

    steps:
      - name: "Checkout code"
        uses: actions/checkout@v4

      - name: "Set up CodeQL"
        uses: github/codeql-action/init@v3
        with:
          languages: "auto" # Automatically detect languages

      - name: "Perform CodeQL Analysis"
        uses: github/codeql-action/analyze@v3
        with:
          category: "security"

      - name: "Run Semgrep for SAST"
        uses: returntocorp/semgrep-action@v2
        with:
          config: "auto" # Automatically detect rules based on the codebase

      - name: "Upload Semgrep Results"
        uses: actions/upload-artifact@v4
        with:
          name: "semgrep-results"
          path: "semgrep.sarif"

      - name: "Run Bandit for Python SAST"
        if: "contains(github.event.head_commit.message, 'python')"
        run: |
          pip install bandit
          bandit -r . -f json -o bandit-results.json

      - name: "Upload Bandit Results"
        if: "contains(github.event.head_commit.message, 'python')"
        uses: actions/upload-artifact@v4
        with:
          name: "bandit-results"
          path: "bandit-results.json"

      - name: "Run ESLint for JavaScript/TypeScript SAST"
        if: "contains(github.event.head_commit.message, 'javascript') || contains(github.event.head_commit.message, 'typescript')"
        run: |
          npm install -g eslint
          eslint . -f json -o eslint-results.json

      - name: "Upload ESLint Results"
        if: "contains(github.event.head_commit.message, 'javascript') || contains(github.event.head_commit.message, 'typescript')"
        uses: actions/upload-artifact@v4
        with:
          name: "eslint-results"
          path: "eslint-results.json"

      - name: "Run Gosec for Go SAST"
        if: "contains(github.event.head_commit.message, 'go')"
        run: |
          curl -sfL https://raw.githubusercontent.com/securego/gosec/master/install.sh | sh
          ./bin/gosec ./...

      - name: "Upload Gosec Results"
        if: "contains(github.event.head_commit.message, 'go')"
        uses: actions/upload-artifact@v4
        with:
          name: "gosec-results"
          path: "gosec.sarif"
```
