# claude-mem Portainer deployment

Use this branch as the deployment source:
- Repository: https://github.com/paulsperfectpc/claude-mem.git
- Repository reference: refs/heads/portainer
- Compose path: compose.yml

This branch contains deployment files only, so Portainer's Git security check
does not encounter application-repository symlinks. Keep this branch separate
from main when syncing the fork with upstream.

The application build uses the upstream v15.4.0 release, matching the server
version observed before the stack was removed. Its Dockerfile builds the worker;
the Compose entrypoint selects SQLite and Claude subscription authentication.

The existing external Docker volumes must already exist:
- claude_mem_runtime: /data/claude-mem, including claude-mem.db
- claude_mem_subscription_home: /home/node, including the Claude login

Do not delete these volumes or restore an older database over them. Make a fresh
backup before recreating the container. A missing external volume intentionally
fails deployment instead of silently creating an empty replacement.

Optional Portainer stack variable: CLAUDE_MEM_BIND_IP=10.254.254.220.
No API key is required. GitOps updates track this deployment branch; upstream
application updates require an explicit change to the release in compose.yml.
