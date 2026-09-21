# ToDo Row Org - User Guide

This is the walkthrough. [`README.md`](README.md) explains *what* ToDo Row Org is and *why* it's built the way it is; this guide is about *where to click* - the first session, start to finish, plus the handful of tools you'll come back to once you're past the first session.

It doesn't narrate every single click. Screens that are self-explanatory once you've seen them once (a checklist, a search box) get a sentence, not a recording. The ones where "where do I even start" is the real question get a GIF.

Here's where this walkthrough ends up - four moments worth knowing exist before you read eleven numbered steps to get there:

<!-- HOOK GRID: same four panels as README.md's opening hook - reuse those exact files, same specs. See docs/internal/GIF_ASSET_CHECKLIST.md, "Hook grid" section. -->
<table>
  <tr>
    <td align="center" width="50%">
      <img src="media/screenshots/PLACEHOLDER-hook-interaction-badges.gif" width="100%" alt="A flat relationship line turning into a labeled Interaction Badge on hover"><br>
      <b>Interaction Badges</b><br>
      A line says two things are connected. This says <i>how</i>.
    </td>
    <td align="center" width="50%">
      <img src="media/screenshots/PLACEHOLDER-hook-vr-blueprint.gif" width="100%" alt="A validation rule's formula rendered as a flowchart with AND/OR junctions"><br>
      <b>VR Blueprint</b><br>
      A validation rule's formula, as an actual flowchart.
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <img src="media/screenshots/PLACEHOLDER-hook-flow-blueprint.gif" width="100%" alt="A Flow's decision branches rendered as a labeled block diagram"><br>
      <b>Flow Blueprint</b><br>
      A Flow's own logic, rendered directly - not reverse-engineered from XML.
    </td>
    <td align="center" width="50%">
      <img src="media/screenshots/PLACEHOLDER-hook-quick-load-app.gif" width="100%" alt="Quick Load App populating a canvas with one click"><br>
      <b>Quick Load App</b><br>
      One click - a whole Salesforce app's metadata, on the canvas.
    </td>
  </tr>
</table>

## Contents

- [Before you start](#before-you-start)
- [1. Install](#1-install)
- [2. Open the workspace](#2-open-the-workspace)
- [3. Connect an org](#3-connect-an-org)
- [4. Load something onto the canvas](#4-load-something-onto-the-canvas)
- [5. Read a node](#5-read-a-node)
- [6. Pull in related objects](#6-pull-in-related-objects)
- [7. Arrange the canvas](#7-arrange-the-canvas)
- [8. Inspect a validation rule](#8-inspect-a-validation-rule)
- [9. Inspect a Flow](#9-inspect-a-flow)
- [10. Find things in a big org](#10-find-things-in-a-big-org)
- [11. Setup Guide and Retrieve Metadata](#11-setup-guide-and-retrieve-metadata)
- [Where everything lives](#where-everything-lives)
- [Troubleshooting](#troubleshooting)

## Before you start

You need three things: VS Code 1.106+, the [Salesforce CLI](https://developer.salesforce.com/tools/salesforcecli) (`sf`, v2.x) on your `PATH`, and a folder with a `sfdx-project.json` at its root open in VS Code. Nothing else - no build step, no config file to fill in first.

Canvas browsing, object exploration, and every tab on a node work fully offline, straight from your local source. You only need a connected org for the handful of things that literally reach out to one: Org Bridge, Quick Load, Retrieve, the Validation Rule active-toggle, and any "Jump to org" link.

## 1. Install

From the Extensions panel (`Ctrl/Cmd+Shift+X`): search "ToDo Row Org", Install. Or from a terminal:

```
code --install-extension ToDoRow.todo-row-org
```

## 2. Open the workspace

Look for the ToDo Row Org icon in the Activity Bar - the vertical icon strip on the far left edge of VS Code, same place as the Explorer and Source Control icons. Click it to open the **Quick Actions** panel, then click **Open Workspace**.

The same action is also in the Command Palette (`Ctrl/Cmd+Shift+P`) as "ToDo Row Org: Open Workspace." Either path scans `force-app/main/default` the first time (a progress indicator shows while that runs) and opens the canvas - an empty grid at this point, because nothing has been loaded onto it yet. That's expected; scanning builds the dependency index in the background, it doesn't place anything.

<!-- PLACEHOLDER (GIF): click the Activity Bar icon, Quick Actions panel opens, click "Open Workspace", canvas panel opens with the scan-progress indicator briefly visible - orients a first-time user to where the extension even lives -->
![Opening the workspace from the Activity Bar](media/screenshots/PLACEHOLDER-guide-open-workspace.gif)

## 3. Connect an org

Click the org indicator chip in the canvas's top bar (it reads "Not connected" until you do this), or choose **Connect Org...** from Quick Actions. Pick Production or Sandbox under "Connect via Browser" - this opens your default browser for the normal Salesforce login screen, exactly like `sf org login web`. The Salesforce CLI holds the session; the extension only asks it for a token when it needs one.

Once connected, the project stays bound to that org (**Locked Org Mode**) until you explicitly disconnect - there's no dropdown silently pointed at a different org mid-session. If you open a project that's already authenticated via the CLI, this step is often skipped automatically: the org indicator shows connected the first time you open the workspace.

<!-- PLACEHOLDER (GIF): click the org chip, Org Bridge dialog opens, click "Connect via Browser" → Production, browser tab opens to the Salesforce login page, switch back to VS Code and the chip now shows the connected org - shows the full round trip once -->
![Connecting an org via the browser](media/screenshots/PLACEHOLDER-guide-connect-org.gif)

## 4. Load something onto the canvas

The fastest path to a populated canvas is **Quick Load App…**, from either Quick Actions or the drawer menu (☰, top-left of the canvas). Pick a Salesforce app your org already has, and it pulls that app's entire declared footprint - its objects, their fields and validation rules, its tabs, and the Apex triggers bound to those objects - onto the canvas in one action.

**Quick Load…** is the more deliberate alternative: a tabbed dialog across six metadata types (Custom Object, Standard Object, LWC, Apex Class, Trigger, Flow), each with its own search and multi-select, for when you know exactly what you want instead of an app's whole footprint.

<!-- PLACEHOLDER (GIF): open Quick Load App, pick one CustomApplication, watch its objects populate the canvas with connection lines already drawn between related ones - the single most important "aha" moment in the whole tool -->
![Quick Load App populating the canvas from one selected app](media/screenshots/PLACEHOLDER-guide-quick-load-app.gif)

## 5. Read a node

Every object lands on the canvas as a node with a colored header band and a row of small icons - type indicator, alert (only shows if something needs attention), hide, lock, jump-to-org, and Reverse Relationships (covered in the next section). Below the header, tabs across the bottom - Fields, SOQL, LWC, Apex Classes, Triggers, Flows, Validation Rules - switch what the node's body shows. All of it comes from the local dependency index built in step 2: if a class shows up under an object's Apex tab, the index found that reference in your actual source.

Wherever the index found a specific operation - a SOQL query, a `@wire`, a DML statement, a Flow element - it's tagged with a small colored **Interaction Badge** (Create, Read, Filter, Bulk, and 25 others) instead of just a bare line connecting two things. Hover one to see exactly what it means.

Not shown here as a GIF - hovering across a row of badges is worth trying directly on your own object's Apex or SOQL tab the first time; it reads faster live than in a recording.

## 6. Pull in related objects

Two different ways to bring a related-but-not-yet-visible object onto the canvas:

- **Connector endpoints.** Every Lookup/Master-Detail line ends in a small circle at each object. Click the circle on the side of the object that's already on your canvas, and the object it points to appears next to it - no need to go find it in Quick Load separately.
- **Reverse Relationships.** The lookup-icon header button opens a popup listing objects that reference *into* the current one - the direction a plain relationship line doesn't show you by default. From there, **Load Related from Org…** queries the connected org's live schema for child relationships your local source scan alone wouldn't surface (managed-package objects, anything outside scan scope), filtered down to real custom relationships so you're not wading through Salesforce's own internal change-tracking objects.

<!-- PLACEHOLDER (GIF): click a connector endpoint to pull one related object onto the canvas, then click the Reverse Relationships header icon on a different object and click "Load Related from Org…" to show a second object appearing from the live org query -->
![Pulling related objects onto the canvas via connector endpoints and Load Related from Org](media/screenshots/PLACEHOLDER-guide-related-objects.gif)

## 7. Arrange the canvas

Drag any node by its header to reposition it - positions persist to `.vscode/tdrorg-layout.json` in your workspace, so they're still there next time you open the project. Once you've loaded more than a handful of objects, **Auto-Arrange** (drawer menu ☰ → Layout) lays everything out for you: objects that relate to each other cluster together with a clean flow-direction layout, and objects with no relationship to anything currently on screen get pulled into their own grid section below, instead of being scattered wherever they happened to land.

The same Layout submenu also has Fit to content, Center origin, Reset zoom, and grid/axes toggles for the viewport itself.

<!-- PLACEHOLDER (GIF): open the drawer menu, click Layout → Auto-Arrange on a canvas with ~8 loosely scattered objects, watch them snap into relationship clusters plus a separate isolated-objects grid -->
![Auto-Arrange laying out a canvas of scattered objects into relationship clusters](media/screenshots/PLACEHOLDER-guide-auto-arrange.gif)

## 8. Inspect a validation rule

Open an object's **Validation Rules** tab and click the Schema icon on any rule's card to open **VR Blueprint** - a modal that parses the rule's formula into an actual syntax tree and lays it out as a flowchart: Event → Conditions → Junctions → Actions. AND/OR junctions are their own visible nodes, not something you have to reconstruct from bracket-nesting, and True/False paths are color-coded so you can trace which branch fires without doing the boolean algebra by eye.

<!-- PLACEHOLDER (screenshot): VR Blueprint modal open on a multi-condition validation rule, showing at least one AND/OR junction node and both a True and a False colored path - this is the one feature with no equivalent in Schema Builder, worth a clean still image -->
![VR Blueprint flowchart for a validation rule formula](media/screenshots/PLACEHOLDER-guide-vr-blueprint.png)

VR Blueprint is view-only in this beta - see the README's *Pro tier* section for what the editable version adds.

## 9. Inspect a Flow

Same idea, for automation instead of a validation formula: open an object's **Flows** tab and click the Schema icon on any Flow's card to open **Flow Blueprint**. Salesforce's own Flow metadata is already graph-shaped - elements and their connectors - so what you see is a direct rendering of that structure: every Decision or Wait branch, loop, fault path, and scheduled path draws as its own labeled connector instead of a flat list of steps. Click any element for its details - a Decision branch's condition, the object a record operation targets, which Flow a subflow calls.

<!-- PLACEHOLDER (screenshot): Flow Blueprint modal open on a Flow with a multi-branch Decision element, showing labeled output pins for each branch plus the default path -->
![Flow Blueprint flowchart with a branching Decision element](media/screenshots/PLACEHOLDER-guide-flow-blueprint.png)

Also read-only in this beta, same boundary as VR Blueprint - for understanding a Flow at a glance, not editing it.

## 10. Find things in a big org

**Object Explorer** (Quick Actions, or the 🔍 icon in the drawer menu) is a searchable list of every object the extension has scanned - a multi-letter filter, a "locked fields only" filter, per-object show/hide, and a **Go to** action that centers the canvas on that object instead of you hunting for it by eye. Not shown as a GIF - it's a plain filtered list, faster to try once than to watch.

## 11. Setup Guide and Retrieve Metadata

Two more dialogs worth knowing exist, both reachable from the drawer menu:

- **Setup Guide** - a 34-item checklist across 7 categories covering the parts of a Salesforce org that never show up in a file (sharing rules, SSO, business hours, and the like). Each item links to the right Setup page; some verify automatically against the connected org.
- **Retrieve Metadata** - wraps the Salesforce CLI's retrieve command behind category filters and live search, for pulling a specific slice of metadata without memorizing `sf` flags.

## Where everything lives

Four entry points, same underlying commands:

- **Activity Bar → Quick Actions** - the 7 commands you'll use to get started each session (Open Workspace, the two Quick Load variants, Object Explorer, Fit Content, Connect Org, Reset Layout).
- **Command Palette** (`Ctrl/Cmd+Shift+P`, type "ToDo Row Org") - the same 7 commands, for keyboard-first workflows.
- **Drawer menu** (☰, top-left of the canvas) - everything above plus canvas-specific tools: Layout (Auto-Arrange, viewport controls), Setup Guide, Retrieve Metadata, and more.
- **Per-node header icons and the right-click / ⋮ menu on a node** - actions scoped to one object: hide, lock, jump to org, reverse relationships, and node-specific layout actions.

## Troubleshooting

- **"Related Objects load failed" or similar org-query errors** - usually means the connected org session expired. Reconnect via the org chip.
- **A connector line looks like it's pointing nowhere** - click Auto-Arrange (see step 7) to force a full redraw, or drag the node slightly; both recompute line geometry from scratch.
- **An object won't disconnect from the wrong org** - Locked Org Mode is intentional (step 3). Use the explicit Disconnect action in Org Bridge, not the org chip's picker.
- Known gaps that are gaps on purpose, not bugs - LWC dynamic-import scanning, Quick Load App's tab-to-object resolution being heuristic, and a few others - are listed in the README's *Known limitations* section, not repeated here.
- Anything not covered above: [open an issue](https://github.com/ShamansIT/todo-row-org-issues/issues).
