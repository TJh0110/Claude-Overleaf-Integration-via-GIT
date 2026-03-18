---
name: overleaf-sync
description: Connect an Overleaf project to a local git repo using the Overleaf git bridge. Use when the user wants to connect Overleaf to git, sync a LaTeX paper, set up a new repo for an Overleaf project, or pull/push changes between local and Overleaf.
---

# Overleaf Git Bridge Skill

Set up a local git repository connected to an Overleaf project via the Overleaf git bridge, then pull all project files and create a CLAUDE.md for future sessions.

## Prerequisites

The user needs:
- An Overleaf account with **Premium** (git bridge requires Premium or higher)
- Their **Overleaf project URL** (e.g. `https://www.overleaf.com/project/abc123...`)
- A **git token** from Overleaf (Account Settings → Git Integration → Generate Token), OR their Overleaf email + password

## Workflow

Make a todo list for all tasks and work through them one by one.

### 1. Gather information

Ask the user for the following (can ask all at once):
- Overleaf project URL or project ID
- Name for the new local repository directory
- Git token (preferred) or Overleaf email + password for authentication

Extract the project ID from the URL: the last path segment of `https://www.overleaf.com/project/<PROJECT_ID>`.

### 2. Create and initialise the local repo

```bash
mkdir -p "/path/to/<repo-name>"
cd "/path/to/<repo-name>"
git init
```

Use the current working directory's parent as the default unless the user specifies otherwise.

### 3. Configure the Overleaf remote

If the user provided a **git token**:
```bash
git remote add origin https://git:<TOKEN>@git.overleaf.com/<PROJECT_ID>
```

If the user provided **email + password** (less secure, prompts each time):
```bash
git remote add origin https://git.overleaf.com/<PROJECT_ID>
git config credential.helper store
# Credentials will be prompted on first pull
```

Verify:
```bash
git remote -v
```

### 4. Pull the project files from Overleaf

```bash
git pull origin master
```

If this fails due to network restrictions in the current environment, inform the user that the repo and credentials are configured — they can run `git pull origin master` manually from a machine with Overleaf access.

If it succeeds, list the pulled files:
```bash
ls -la
```

### 5. Create CLAUDE.md

Create a `CLAUDE.md` in the new repo root with project context:

```markdown
# <Repo Name>

LaTeX paper project synced with Overleaf via the Git bridge.

## Overleaf sync

- **Overleaf project:** https://www.overleaf.com/project/<PROJECT_ID>
- **Git bridge remote:** configured as `origin` (token auth embedded)

Pull latest before working:
```bash
git pull origin master
```

Push changes back to Overleaf when done:
```bash
git add .
git commit -m "describe changes"
git push origin master
```

## Working with Claude Code

Ask Claude to:
- Edit or rewrite sections of `.tex` files
- Add or fix BibTeX references in `.bib` files
- Restructure the paper or improve writing clarity
- Fix LaTeX compilation errors
- Format tables, figures, and equations

## Project structure

(Update once files are pulled from Overleaf)
- `main.tex` — main document entry point
```

### 6. Commit the CLAUDE.md

```bash
git add CLAUDE.md
git commit -m "Add CLAUDE.md with project context and Overleaf workflow"
```

### 7. Summary

Provide the user with a summary in this format:

---
**Overleaf git repo set up successfully.**

- Local repo: `/path/to/<repo-name>`
- Overleaf remote: `https://git.overleaf.com/<PROJECT_ID>`
- Files pulled: ✅ / ⚠️ (manual pull needed — network restriction in this env)
- CLAUDE.md created: ✅

**Day-to-day commands:**

| Action | Command |
|--------|---------|
| Pull latest from Overleaf | `git pull origin master` |
| Push changes to Overleaf | `git push origin master` |
| Open Claude Code here | `claude` (run inside the repo folder) |

**Tip:** Open Claude Code inside this folder and ask it to edit your `.tex` files directly. Push when done — changes appear in Overleaf immediately.
---
