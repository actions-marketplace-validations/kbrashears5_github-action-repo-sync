<h1 align="center">github-action-file-sync</h1>

<div align="center">
    
<b>Github Action to sync files across repos</b>
</div>

# Use Cases
Keep the github metadata in sync with your code! Metadata is now configuration as code, and can be validated with a Pull Request.

# Setup
Create a new file called `/.github/workflows/repo-sync.yml` that looks like so:
```yaml
name: Repo Sync

on:
  push:
    branches:
      - master
  schedule:
    - cron: 0 0 * * *

jobs:
  file_sync:
    runs-on: ubuntu-latest
    steps:
      - name: Fetching Local Repository
        uses: actions/checkout@master
      - name: Repo Sync
        uses: kbrashears5/github-action-repo-sync@v1.0.0
        with:
          TYPE: npm
          PATH: package.json
          TOKEN: ${{ secrets.ACTIONS }}
```
## Parameters
| Parameter | Required | Description |
| --- | --- | --- |
| TYPE | true | Type of repo. See below for supported repo types |
| PATH | true | Path to the repo type's metadata file |
| TOKEN | true | Personal Access Token with Repo scope

## Supported Repo Types
| Repo Type | File |
| --- | --- |
| npm | package.json |
| nuget | ProjectName.csproj |