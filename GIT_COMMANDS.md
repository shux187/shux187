# Exact Commands to Apply This Profile Update (Windows / PowerShell)

You have `git` installed but not `gh` (GitHub CLI) or `jq` — so this version skips both and does
everything through plain `git` plus the GitHub website. If you install `gh` later, the shorter
`gh`-based version is at the bottom, but you don't need it.

## 0. Get the full repo list manually (no `gh`/`jq` needed)

Open **https://github.com/shux187?tab=repositories** in your browser (you're logged in, so this
works even though it was blocked for automated fetching). Note down the real name/URL for each
repo that matches a project in `README.md` and `docs/portfolio-map.md`, then replace every
`TODO: confirm repo link` in those files with the real link. Do this in a text editor (Notepad,
VS Code) — it's a find-and-replace job, not a command.

## 1. Create the profile repo on GitHub.com (do this in the browser, not PowerShell)

`github.com/shux187/shux187` doesn't exist yet, so this is a first-time setup:

1. Go to **https://github.com/new**
2. Repository name: `shux187` (must exactly match your username)
3. Set to **Public**
4. Leave "Add a README file" **unchecked**
5. Click **Create repository**

## 2. Extract the zip I sent you

Right-click `shux187-profile.zip` (wherever your browser downloaded it — usually
`C:\Users\ASSETWISE\Downloads`) → **Extract All** → extract it. You should end up with a folder
like:

```
C:\Users\ASSETWISE\Downloads\shux187-profile\
```

containing `README.md`, `assets\`, `docs\`, `.github\`, `GIT_COMMANDS.md`, `SECURITY_CHECKLIST.md`.

## 3. Push it, in PowerShell

Open PowerShell and run these one at a time (adjust the `cd` path if you extracted it somewhere
other than Downloads):

```powershell
cd $HOME\Downloads\shux187-profile
git init
git remote add origin https://github.com/shux187/shux187.git
git add .
git commit -m "Rebuild profile README as a Blockchain + AI engineering portfolio"
git branch -M main
git push -u origin main
```

If it asks you to sign in, a browser window will pop up — log in there and it'll continue.

If `git push` fails with something about the remote already having content (it shouldn't, since
you just created an empty repo), run `git pull origin main --allow-unrelated-histories` first,
resolve any conflict, then push again.

## 4. Update your GitHub profile bio/fields (browser only)

Go to **Settings → Public profile**:

- **Bio**: `Blockchain Developer & AI/ML Engineer | Solidity · Rust · Python · Smart Contract Security · Web3` — two alternates are in `README.md`'s "Profile Bio Options" section.
- **Location**: confirm it says `Lusaka, Zambia`.

## 5. Turn on repo security features (browser only, per repo)

For each repo you're featuring: **Settings → Security** on that repo →

- Turn on **Dependabot alerts** and **Dependabot security updates**
- Turn on **Secret scanning** (free on public repos)
- Set up **Code scanning** (CodeQL) via the suggested default workflow

## 6. Wire up the security scan workflow on a Solidity repo

Once you know which repo has your Solidity contracts:

```powershell
cd C:\path\to\that\repo          # wherever you cloned that specific repo
mkdir .github\workflows -Force
Copy-Item "$HOME\Downloads\shux187-profile\.github\workflows\solidity-security-scan.yml" .github\workflows\
git add .github\workflows\solidity-security-scan.yml
git commit -m "Add Slither security scan workflow"
git push
```

Edit the `target:` line inside that yml file first if your contracts live somewhere other than
a `contracts/` folder.

## 7. Set pinned repositories (browser only)

Go to `github.com/shux187` → **Customize your pins**. Use the 6 slots recommended in `README.md`
under "Pinned Repository Strategy," once you've matched project names to real repo names from
step 0.

---

## If you install GitHub CLI later (optional, shortens steps 0/1/5)

Install with `winget install --id GitHub.cli` in PowerShell, then `gh auth login`. After that:

```powershell
gh repo list shux187 --limit 100 --json name,description,url,primaryLanguage,stargazerCount | ConvertFrom-Json | Format-Table name, url, description

gh repo create shux187/shux187 --public --description "Blockchain Developer & AI/ML Engineer" --add-readme=false

gh api -X PUT repos/shux187/<repo-name>/vulnerability-alerts
gh api -X PUT repos/shux187/<repo-name>/automated-security-fixes
```

`ConvertFrom-Json | Format-Table` replaces the `jq` step — PowerShell parses JSON natively, no
extra tool needed.
