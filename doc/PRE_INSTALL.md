# Pre-installation Warnings

⚠️ **This is a very heavy application.** Here's what you should know:
- It requires **4 containers** (Twenty Server, Twenty Worker, PostgreSQL, Redis).
- Due to Node.js backend internals, it typically needs **over 2GB+ of available RAM**.
- It bundles its own database inside Docker.
- Backups require stopping all containers (downtime).
- You **cannot install** this onto a sub-path domain. It must sit on its own dedicated domain (e.g., `twenty.myyunohost.com`).

Please confirm you understand these constraints and resource obligations before continuing to install.
