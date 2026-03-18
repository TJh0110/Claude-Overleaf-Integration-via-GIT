# Overleaf Git Setup Guide and Claude_Skill.md

## Repository

Local path: `/path/to/<YOUR-PROJECT-NAME>`
Overleaf project: `https://www.overleaf.com/project/<YOUR-PROJECT-ID>`
Git bridge remote: `https://git.overleaf.com/<YOUR-PROJECT-ID>`

## First-time setup

### 1. Create the local repo

```bash
mkdir -p "/path/to/<YOUR-PROJECT-NAME>"
cd "/path/to/<YOUR-PROJECT-NAME>"
git init
git remote add origin https://git.overleaf.com/<YOUR-PROJECT-ID>
```

### 2. Pull from Overleaf

```bash
git pull origin master
```

You will be prompted for credentials:
- **Username:** your Overleaf email address
- **Password:** your Overleaf password

> If you use two-factor authentication (2FA), generate a git token at:
> Overleaf → Account Settings → Git Integration → Generate Token
> Use the token as your password.

To avoid entering credentials every time, cache them:

```bash
git config credential.helper store
```

Or embed a token directly in the remote URL (keep this private):

```bash
git remote set-url origin https://git:<YOUR-GIT-TOKEN>@git.overleaf.com/<YOUR-PROJECT-ID>
```

## Day-to-day workflow

| Action | Command |
|--------|---------|
| Pull latest from Overleaf | `git pull origin master` |
| Push local changes to Overleaf | `git push origin master` |
| Check status | `git status` |
| View history | `git log --oneline` |

## Notes

- Overleaf's Git bridge uses the `master` branch by default.
- Changes pushed here will appear immediately in the Overleaf editor.
- Changes made in Overleaf must be pulled before you can push (standard git merge rules apply).
- The Git bridge requires an Overleaf **Premium** subscription or higher.
