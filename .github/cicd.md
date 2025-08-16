name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run CodeQL Analysis
        uses: github/codeql-action/init@v2
        with:
          languages: typescript, javascript
      - name: Run DAST Scan
        uses: zaproxy/action-full-scan@v0.4.0
        with:
          target: ${{ env.TEST_URL }}

  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - name: Install dependencies
        run: npm ci
      - name: Run unit tests
        run: npm run test:unit
      - name: Run integration tests
        run: npm run test:integration
      - name: Run Cucumber tests
        run: npm run test:e2e

  database-deploy:
    runs-on: ubuntu-latest
    needs: [security-scan, test]
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to SQL MI
        uses: azure/sql-action@v1
        with:
          server-name: ${{ secrets.SQL_SERVER_NAME }}
          connection-string: ${{ secrets.SQL_CONNECTION_STRING }}
          dacpac-package: './database/database.dacpac'
