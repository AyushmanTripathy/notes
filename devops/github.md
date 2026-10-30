# Github

## Action

- single reusable command
- Written as code (js or docker) with action.yml file
- Can be seprate repo or github marketplace
- Trigger when called by a step in the workflow

### Composite Action

- package multiple workflow steps into a reusable action
- needs to be added into `.github/actions/build/action.yml`

```yaml
name: Build Application
description: Install dependencies, test, and build

runs:
  using: composite
  steps:
    - name: Install dependencies
      run: npm ci
      shell: bash

    - name: Run tests
      run: npm test
      shell: bash

    - name: Build
      run: npm run build
      shell: bash
```

## Workflow

- Overall pipeline
- Written as yml files in ex: `.github/workflows/ci.yml`
- triggered by events ex. push, pull_request etc

```yaml
name: Node.js CI

on:
  push:
    branches: [ "main", "develop" ]
  pull_request:
    branches: [ "main" ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      # Composite action
      - name: Build application
        uses: ./.github/actions/build
```


### workflow_dispatch

- Allows triggering workflow from Github UI (Action tab), CLI ot Rest API.
- it can specify inputs, that can be used in jobs

```yaml
name: Parameterized Workflow

on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Target deployment environment'
        required: true
        default: 'staging'
        type: choice
        options:
          - development
          - staging
          - production
      deploy_debug:
        description: 'Enable debug logging'
        required: false
        default: false
        type: boolean

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Output selected parameters
        run: |
          echo "Deploying to environment: ${{ inputs.environment }}"
          echo "Debug mode enabled: ${{ inputs.deploy_debug }}"
```

Terms
=====

1. __Promoting__, means taking a build image and moving to next enviroment without rebuilding
2. __repository_dispatch__, triggers a workflow from outside github
