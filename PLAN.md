# dbt Documentation Automation Plan

## Goal
Auto-generate documentation for dbt projects (starting with RMI tables from `rj-crm-registry`) using a simple, reusable system.

## What We're Building
- **Input**: dbt models from GitHub repositories
- **Output**: Mintlify documentation pages with table schemas, column descriptions, and usage examples
- **Trigger**: Automatic rebuild on repository changes

## Core Components

### 1. Configuration (`config/projects.yml`)
```yaml
projects:
  rmi:
    repository: "prefeitura-rio/queries-rj-crm-registry"
    models_path: "models/core"
    table_pattern: "rmi_*"
    display_name: "RMI (Registro Municipal Integrado)"
```

### 2. GitHub Fetcher (`scripts/dbt_docs_generator.py`)
- Fetch `.sql` and `.yml` files from configured repositories
- Parse dbt model metadata and column definitions
- Generate documentation pages using templates

### 3. GitHub Actions

#### Docs Repository (`.github/workflows/update-dbt-docs.yml`)
- Runs weekly or on repository changes
- Rebuilds all documentation to ensure consistency
- Updates navigation structure automatically

#### Source Repository Trigger (`.github/workflows/trigger-docs-update.yml`)
```yaml
name: Trigger Documentation Update

on:
  push:
    branches: [ master, main ]
    paths:
      - 'models/**'
      - 'dbt_project.yml'

jobs:
  trigger-docs:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger documentation update
        uses: peter-evans/repository-dispatch@v2
        with:
          token: ${{ secrets.DOCS_UPDATE_TOKEN }}
          repository: prefeitura-rio/mintlify-docs
          event-type: dbt-schema-updated
          client-payload: |
            {
              "repository": "${{ github.repository }}",
              "ref": "${{ github.ref }}",
              "sha": "${{ github.sha }}"
            }
```

### 4. Template System
- Standard MDX templates for table documentation
- Includes schema info, column details, and municipal context
- Generates navigation structure dynamically

## Implementation Steps

### Week 1: Foundation
- Create configuration system for projects
- Build GitHub API fetcher for dbt files
- Design documentation templates

### Week 2: Automation
- Implement GitHub Actions workflow
- Set up webhook triggers from source repositories
- Generate initial RMI documentation

### Week 3: Enhancement
- Add interactive schema explorer
- Create common query templates
- Implement monitoring and health checks

## Benefits
- **Simple**: No complex change detection - always rebuild everything
- **Reliable**: Full rebuild prevents documentation drift
- **Reusable**: Easy to add new dbt projects via configuration
- **Maintainable**: Single system for all documentation needs