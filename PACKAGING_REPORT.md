# YunoHost Package Report: twenty_ynh

## Status: 🟡 Needs Manual Steps

## What Was Generated
- [x] manifest.toml
- [x] All scripts (install, remove, upgrade, backup, restore)
- [x] conf/nginx.conf
- [x] conf/systemd.service
- [x] App config template (docker-compose & .env)
- [x] tests.toml
- [x] doc/DESCRIPTION.md
- [ ] doc/screenshots/ (you must add a screenshot)

## Decisions Made
| Decision | Choice | Reason |
|---|---|---|
| Complexity | 🔴 | Very heavy app. 4 services (Node/Server, Node/Worker, Postgres, Redis). Requires > 2GB RAM. |
| Strategy | docker-wrap | Compiling Twenty natively (NextJS, BullMQ, Redis, Postgres) is impractical and brittle for a standard package. Docker wrapping encapsulates its complexity nicely. |
| LDAP | false | Upstream lacks built-in direct LDAP config for standard YunoHost mapping; mostly relies on OIDC/OAuth or internal users. |
| SSO | false | Same as above. YunoHost SSO still protects the app route natively if made private. |
| Database | bundled-in-docker | App requires Postgres 16 with multiple specific configs. Let upstream docker compose handle it to avoid difficult migrations. |
| Subpath | domain-only | SPAs and CRMs with frontend configs often break on YH subpaths. Subpath installation is disabled for reliability. |
| Architectures | all | Docker images might be amd64/arm64 depending on upstream release tags. |

## ⚠️ Items Requiring Human Action
1. Add screenshots to `doc/screenshots/`.
2. Check if your server has enough RAM: Minimum 4GB+ recommended. Avoid deploying this on 1GB VPS or it will OOM-kill easily.

## 🔍 Potential Issues
- **Downtime during Backups**: Since PostgreSQL runs inside Docker, the `scripts/backup` STOPS the docker containers, dumps the volumes, and restarts them. This is the only safe way to ensure database consistency for docker-wrapped stateful services. Expect a brief 1-2 minute downtime during YunoHost scheduled backups.
- **Root access**: Docker compose operates on the root socket, so the systemd service runs as `root`.
- **Database Opacity**: YunoHost cannot help you maintain or run queries on this Postgres DB via `ynh_mysql` tools because it is hidden inside the docker bridge network.

## Next Steps to Publish
1. Test on a YunoHost instance: `sudo yunohost app install /path/to/twenty_ynh --debug`
2. Test backup/restore.
3. Replace the placeholder tag/version in manifest.toml / .env with the current valid tag, if "latest" fails or misbehaves over time.
4. Add nice screenshots to doc/screenshots/
5. Transfer repo to YunoHost-Apps organization and PR to app catalog.
