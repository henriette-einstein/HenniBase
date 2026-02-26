---
type: "[[Note]]"
created: 2026-02-25
modified: 2026-02-25
tags: [howto, git, obsidian, version-control, backup]
sources:
  - "https://github.com/Vinzent03/obsidian-git"
  - "https://forum.obsidian.md/t/the-easiest-way-to-setup-obsidian-git-to-backup-notes/51429"
areas: []
---

This guide explains how to connect an Obsidian vault to a remote Git repository using the **Obsidian Git** community plugin (by Vinzent03). Once set up, the plugin automates committing and syncing your vault, giving you a full version history and an off-site backup on GitHub or any other Git host.

## Prerequisites

The following must be in place before installing the plugin.

- Git is installed on your system (`git --version` should return a version number)
- A GitHub (or GitLab / Gitea) account exists and a remote repository has been created for the vault
- Git is configured with a name and email address:
  ```
  git config --global user.name "Your Name"
  git config --global user.email "you@example.com"
  ```
- Authentication to the remote is working, either via SSH key or a personal access token stored in the system credential manager

## Initialising the Repository

Open a terminal inside the vault's root folder and run the following commands to create a local repository and link it to the remote.

```
git init
git remote add origin https://github.com/<username>/<repo>.git
git branch -M main
```

Before the first commit, create a `.gitignore` file in the vault root. The Obsidian configuration folder contains local settings that generally should not be shared, so the following baseline is recommended:

```
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.trash/
.DS_Store
```

If you want to synchronise plugin settings, snippets, or themes across devices, you can remove those specific paths from the ignore file. After creating the `.gitignore`, stage everything and push:

```
git add .
git commit -m "Initial commit"
git push -u origin main
```

## Installing the Plugin

Open Obsidian and navigate to Settings → Community Plugins. Disable Safe Mode if prompted, then click Browse and search for **Obsidian Git**. Install it and enable it. The plugin may display a "Git is not ready" warning until it has verified that Git is accessible. If this persists, check that Git is available on the system PATH.

## Configuring the Plugin

Open Settings → Obsidian Git. The most important options are:

- **Vault backup interval**: the number of minutes between automatic commits and pushes. A value between 10 and 30 minutes works well for active use. Set to 0 to disable auto-backup and commit manually instead.
- **Auto pull interval**: how frequently the plugin pulls from the remote. Useful when the vault is open on multiple devices.
- **Commit message**: the template for auto-generated commit messages. The default includes a timestamp, which produces a clean history.
- **Pull updates on startup**: enabling this ensures the vault is up to date each time Obsidian opens.

## Daily Workflow

Once configured, most interaction with Git happens automatically. For manual control, open the command palette with `Ctrl+P` (Windows/Linux) or `Cmd+P` (macOS) and search for the following commands.

- `Obsidian Git: Commit all changes` — stages all modified files and creates a commit without pushing
- `Obsidian Git: Commit-and-sync` — commits, pulls from the remote, then pushes
- `Obsidian Git: Pull` — fetches and merges changes from the remote without committing local changes
- `Obsidian Git: Open source control view` — opens a sidebar panel showing staged and unstaged changes, equivalent to `git status`
- `Obsidian Git: Open history view` — shows the commit log for the vault or a selected file

The source control view allows individual files to be staged or unstaged before a commit, which is useful when you want fine-grained control over what enters the history.

## Viewing File History and Diffs

The history view shows all commits in reverse chronological order with their messages and timestamps. Selecting a commit reveals the list of files changed in that commit. The diff view (`Obsidian Git: Open diff view`) displays line-level changes for any file. For a more detailed per-file history, the **Version History Diff** community plugin integrates with Obsidian Git and is worth installing alongside it.

## Mobile

On iOS and Android, Obsidian Git uses **isomorphic-git**, a JavaScript reimplementation of Git that does not rely on a native Git binary. This means the plugin works on mobile but with limitations: operations are slower on large vaults, and complex merge scenarios may require resolution on desktop. For mobile use, it is advisable to stage and commit individual files rather than committing all changes at once, and to pull before committing to reduce the risk of conflicts.

Note that the plugin does not function in the Obsidian app installed via Snap on Linux, due to Snap's sandboxing restrictions.

## Resolving Conflicts

Merge conflicts occur when the same file has been modified both locally and on the remote since the last common commit. Obsidian Git marks conflicted files in the source control view. The conflicts must be resolved in a text editor: open the file, locate the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), edit the file to the desired state, save it, then stage and commit the resolved file. Keeping an auto-pull interval active significantly reduces the frequency of conflicts in a single-user setup.

## Connections

- [[Git]] – The underlying version control system the plugin wraps
- [[GitHub]] – The most common remote host used with Obsidian Git for backup and sync
- [[Version Control]] – The broader practice of tracking changes to files over time
