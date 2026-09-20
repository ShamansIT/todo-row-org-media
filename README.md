# ToDo Row Org - Media Assets

Public asset repository for the [ToDo Row Org](https://github.com/ShamansIT/TODO-ROW-ORG) VS Code extension. Contains only GIFs/screenshots referenced by the extension's `README.md`, `USER_GUIDE.md`, and the marketing website - no source code.

This repo exists because the main `TODO-ROW-ORG` repository is private and proprietary; VS Code Marketplace and GitHub rewrite relative image paths in a README to `raw.githubusercontent.com`, which 404s for a private repo's images. This repo is public so those image URLs resolve for anyone viewing the Marketplace listing.

## Structure

```
screenshots/
  PLACEHOLDER-hook-interaction-badges.gif
  PLACEHOLDER-hook-vr-blueprint.gif
  PLACEHOLDER-hook-flow-blueprint.gif
  PLACEHOLDER-hook-quick-load-app.gif
  ... (see the full list and exact filenames in the main repo's
      docs/internal/GIF_ASSET_CHECKLIST.md)
```

File names match exactly what `README.md`/`USER_GUIDE.md` in the main repo reference - once files land here under their real names (drop the `PLACEHOLDER-` prefix only if you also update the reference in the main repo at the same time), the main repo's image links point at:

```
https://raw.githubusercontent.com/ShamansIT/todo-row-org-media/main/screenshots/<filename>
```

## What goes here

Only image/GIF assets used in public-facing ToDo Row Org documentation. Nothing else - no extension source, no internal docs, no demo project data beyond what's visible in a recording.
