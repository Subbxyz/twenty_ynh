# Twenty CRM

The #1 Open-Source CRM.

## What You Can Do With Twenty
- Personalize layouts with filters, sort, group by, kanban and table views
- Customize your objects and fields
- Create and manage permissions with custom roles
- Automate workflow with triggers and actions
- Emails, calendar events, files, and more

## Important Technical Details for YunoHost
- Because Twenty CRM is composed of multiple microservices interacting tightly with a Postgres database and Redis, this app uses a **Docker-wrapping deployment strategy**. 
- It maintains its own internal database opaque to YunoHost built-in db management tools.
- Restarts and backups might induce a short 1-2 minute downtime window since they freeze the Postgres db volume.
