# Open-webui
Open WebUI

Here are all the files I updated:

1. d:\Users\Projects\open-webui\src\lib\components\layout\Sidebar.svelte

Added import { page } from '$app/stores'
Added let showWorkspaceItems = false
Added $: showWorkspaceItems = $page?.url?.pathname?.startsWith('/workspace') ?? false
Replaced the workspace pinned item from a simple link to a collapsible section with Models, Knowledge, Prompts, Skills, Tools sub-items
2. d:\Users\Projects\open-webui\src\routes\(app)\workspace\+layout.svelte

Removed the entire top horizontal nav bar (Models / Knowledge / Prompts / Skills / Tools tabs)
Kept only mobile sidebar toggle + content slot
3. d:\Users\Projects\open-webui\Dockerfile

Uncommented ENV NODE_OPTIONS="--max-old-space-size=4096" to prevent out-of-memory during build
Those are the only 3 files. The changes are confirmed in place — I just verified them above. The issue is purely Docker serving the old cached image. Run this to deploy:



cd d:\Users\Projects\open-webui
docker compose down
docker rmi ghcr.io/open-webui/open-webui:main
docker builder prune -af
docker compose build --no-cache open-webui
docker compose up -d
