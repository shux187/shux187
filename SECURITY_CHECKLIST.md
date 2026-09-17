# Security Checklist Before Publishing

## Secrets exposure — could not be verified from here

This session has no read access to your repos' actual file contents (no GitHub connector, no
authenticated API). **I did not scan any repo for secrets** — don't take this profile rewrite as
a substitute for that. Run this yourself before making anything public or newly prominent:

```bash
# From inside each repo you're about to feature:
pip install detect-secrets --break-system-packages   # or: brew install gitleaks
detect-secrets scan > secrets-report.json
# or, faster and no install if you have Docker:
docker run --rm -v "$PWD:/repo" zricethezav/gitleaks:latest detect --source /repo -v
```

Specifically check the repos going into the featured matrix for:

- [ ] `.env` files committed (should be gitignored, with a `.env.example` instead)
- [ ] Hardcoded private keys / seed phrases in Solidity deploy scripts or test fixtures
- [ ] API keys (Infura/Alchemy/RPC provider keys) hardcoded rather than loaded from env
- [ ] Database connection strings with embedded credentials
- [ ] Any wallet mnemonic committed for "testing convenience"

If `detect-secrets` or `gitleaks` finds something in a repo's history (not just the current
tip), a `git rm` on the latest commit is **not enough** — the secret is still in history. Rotate
the credential first, then use `git filter-repo` (or BFG Repo-Cleaner) to scrub history, and only
then feature that repo in the portfolio.

## Repo hygiene, per featured repo

- [ ] `.gitignore` present and covers `node_modules/`, `.env`, build artifacts, `cache/`, `artifacts/` (Hardhat)
- [ ] `.env.example` present if the repo needs environment variables
- [ ] LICENSE file present (MIT is the common default for portfolio/educational repos)
- [ ] README follows the structure in `docs/portfolio-map.md` / the brief's Section 20-22 templates

## GitHub account-level security (Section 23 of the brief)

- [ ] Dependabot alerts + security updates on for each active repo
- [ ] Secret scanning on (free for public repos)
- [ ] CodeQL set up on at least the Solidity/JS repos going into the featured matrix
- [ ] Branch protection on `main` for any repo with a deploy workflow

None of the above were verified as currently enabled — this session couldn't check repo Settings
pages. Treat every box here as unchecked until you've confirmed it yourself.
