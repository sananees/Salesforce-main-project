# Git Workflow Notes

- Project root: salesforce-main-project
- Package directory: force-app
- Salesforce metadata source: force-app/main/default
- Configuration folder: config
- Manifest file: manifest/package.xml
- Scripts folder: scripts
- Documentation folder: docs
- Local files such as .sf, .sfdx, .env, and secrets should be ignored by Git.

## Source of Truth

The GitHub repository is the team's source of truth because it keeps the approved project files, commit history, and changes made by team members. A Salesforce org can be changed directly and may not show who changed each file. Team members should make changes locally, commit them to Git, and push them to GitHub.