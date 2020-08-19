---
nav_order: 27
title: Workflow
has_children: true
has_toc: false
---

# Standard Deploy Workflows

## Code Up, Content Down
### Applicable projects
- This is standard. Use on ALL projects unless there are special circumstances.
- If this is not being used on a project, document the used workflow in the site manual.

### Overview / Rules
- This is the most common setup for the sites we are managing.
- **WPE Copy Environment to Production should _NOT_ be used.**
- Pantheon has [a video](https://www.youtube.com/watch?v=gw8SYykm8f0)
    that explains a similar workflow.

### Process
- Content is edited on Production.
- Migrate DB Pro + Media Addon are used to sync content _from_ Production _to_ Staging and Dev.
- Code is deployed via Git.
- Code changes are developed locally and Git pushed to Dev.
- When ready for review, git push to Staging.
- When ready for deploy, git push to Production.
- Any content edits necessary for the new code must:
    - Be made on Production and use Migrate DB Pro to copy to other environments.  
        OR
    - Be made on Dev/Staging, and then manually copied over to Prod.
    
## Code Up, Content Up
### Applicable projects
- When there is no visitor input saved in WP.
- When content staging is important for the client.

### Overview / Rules
- This cannot be used if visitor content is used/edited regularly. E.g:
    - Gravity Forms
    - Comments
    - WooCommerce

### Process
- Editing Content
    - Content is edited on Staging.
    - Any content edits made on Production must also be entered on Staging.
        - **Do Not** use WPE Copy Environment from Prod.
        - **Do Not** use Migrate DB Pro to copy content from Production to Staging.
- Editing code
    - Git push to Dev for development.
    - Git push to Staging when ready for client review.
    - Production Git repository is **not** used.
- Deploying to Production
    - Coordinate with all developers and content editors
        to make sure Staging is prepared for deploy.
    - Deploy from Staging using WPE Copy Environment from Staging to Production.
