# claude-mem Portainer deployment

Repository: https://github.com/paulsperfectpc/claude-mem.git
Repository reference: refs/heads/portainer
Compose path: compose.yml

This branch contains deployment files only. Keep it separate from main when
syncing the application fork, so Portainer does not encounter upstream symlinks.

The build uses upstream v15.5.0. The Compose entrypoint runs the SQLite worker
with Claude subscription authentication. No API key is required.

These external Docker volumes must already exist:
- claude_mem_runtime mounts at /data/claude-mem and holds the memory database.
- claude_mem_subscription_home mounts at /home/node and holds the Claude login.

Make a fresh backup before deployment. Do not delete these volumes or restore
an older migration database over the surviving data. Missing external volumes
intentionally fail deployment instead of creating empty replacements.

Optional Portainer stack variable: CLAUDE_MEM_BIND_IP=10.254.254.220.
GitOps updates track this branch; application upgrades require an explicit
release change in compose.yml.
