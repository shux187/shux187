# Portfolio Verification Map

This file exists because the master brief for this profile rewrite has an explicit
**no-fabrication rule**. It records, honestly, what was verified and how, so nothing in
`README.md` is presented with more confidence than the evidence supports.

## What was verified directly from GitHub (public, unauthenticated)

Source: `https://github.com/shux187` profile page, fetched during this session.

- **Bio**: "I'm a software engineering student with mad passion for the Blockchain, AI and
  quantum computers!"
- **Followers**: 29 · **Following**: 54 · **Public repos**: 18 (per profile counter)
- **Popular/pinned repositories** (name — description — language — stars):
  1. `Agent-1` — no description shown — Python — 3 stars
  2. `Tokenized_Real_Estate_Ownership` — "merges technology with real estate, enabling
     fractional ownership" — Solidity — 2 stars
  3. `Building_a_blockchain_in_Python` — implements a blockchain with a RESTful API for
     transactions, mining, and node sync — Python — 1 star
  4. `Asset_Tokenizer` — "Educational Real-World Asset tokenization protocol using Solidity
     and Foundry" — Solidity — 1 star
  5. `My-first-working-JS-project` — memory card matching game — JavaScript — forked
  6. `Smart-Contract-Testing-with-Hardhat` — no description shown — JavaScript — forked
- **Achievements badges shown**: YOLO, Pull Shark, Pair Extraordinaire

## What could not be verified, and why

- GitHub's `?tab=repositories` listing (the full 18-repo list) returned a
  `robots.txt`-disallowed error to automated fetches during this session, so only the 6
  "popular repos" shown on the profile overview were confirmed. The GitHub REST API was also
  not reachable from this environment (blocked at the network/session level).
- `shux187/shux187` (the profile README repo) returned a 404 — **there is currently no profile
  README repo at all**, so this is a *creation*, not an "upgrade" of an existing file.
- Several exact repo-name guesses for the larger project list (`eth-transaction-tracker`,
  `blockchain-node-explorer`, `AgriChain`, `ChainMsg`, `ZedLedger`, `OutSourcer`, `POWCHAIN`,
  `CertChain`) all 404'd — meaning either they're under different slugs, private, or not yet
  pushed under those exact names.

## What's included on the word of the repository owner

During this session, the repo owner confirmed that the ~30 project names referenced in the
brief (ADOS, BADD, OEBP, the Zambia proptech platform, the ZK/crypto research suite, OrchAgent,
CertChain, AgriChain, EventbadgesZM, LinkCardZM, the DAO governance demo, etc.) **are** pushed
to public GitHub repos under `shux187`. Those project names, descriptions, and tech stacks are
used in `README.md` and the docs below — but every repo **link** is marked
`TODO: confirm repo link` because the exact slug could not be independently verified.

**Before publishing**, replace every `TODO: confirm repo link` with the real URL. The fastest
way to get the full list in one shot:

```bash
gh repo list shux187 --limit 100 --json name,description,primaryLanguage,stargazerCount,url,updatedAt,isPrivate
```

Then match each project name above to its real slug and swap in the link. If a named project
turns out to be private, either make it public (if you want it featured) or drop that row from
the table.

## Maturity labels used

🟢 Production-oriented · 🔵 Active development · 🟡 Research prototype · 🟣 Experimental ·
⚪ Educational

No project is labeled 🟢 Production in this rewrite — there's no verified mainnet deployment,
audit, or user base on record. If one of these projects *does* have a real deployment (testnet
or mainnet address, live users), tell me and I'll upgrade that specific row with the evidence
attached (contract address, deployment tx, etc.) rather than a bare label change.
