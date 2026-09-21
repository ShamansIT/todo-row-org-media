# ToDo Row Org - Public Assets

Public asset repository for the [ToDo Row Org](https://marketplace.visualstudio.com/items?itemName=ToDoRow.todo-row-org) VS Code extension (source repo is private - proprietary software, see the extension's own `LICENSE`). Contains GIFs/screenshots and small public documentation files (never source code) referenced by the extension's `README.md` and the marketing website.

## USER_GUIDE.md

A mirror of the main repo's `todo-row-org/USER_GUIDE.md`. Exists here because the main repo is private, and `vsce` rewrites *every* relative link in the extension's README (not just images) to a GitHub blob URL based on the `repository` field - a private repo means that link 404s on the Marketplace listing page. `README.md` in the main repo links to this copy via its full GitHub URL instead of a bare relative `USER_GUIDE.md`.

**Keep this in sync manually**: whenever `todo-row-org/USER_GUIDE.md` changes in the main repo, copy the updated file here too and commit/push. There's no automated sync for this (unlike LICENSE/THIRD-PARTY-NOTICES.md's byte-identity check in the main repo's own release gate).

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

Image/GIF assets used in public-facing ToDo Row Org documentation, and small public documentation files that need a public URL because the main repo is private (currently just `USER_GUIDE.md`). Never extension source code, never internal docs (`docs/internal/`), never demo project data beyond what's visible in a recording.
