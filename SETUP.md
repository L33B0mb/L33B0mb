# Profile setup — the steps I can't do for you

The README and workflows are ready and committed locally. These are the pieces that need
your hands on them, in the order that matters.

---

## 1. Create and push the repo  ← nothing else works before this

A profile README lives in a public repo named exactly after your handle. The commits are
already made; this only creates the remote and pushes.

```bash
cd "/home/vilis/ai projects/Vilis gh prof"
gh repo create L33B0mb/L33B0mb --public --source=. --remote=origin --push
```

`gh` is already authenticated as `L33B0mb` with `repo` + `workflow` scope, so this needs
no login. Afterwards: repo → **Actions** tab → enable workflows → run **Generate
contribution snake** once manually (`workflow_dispatch`) rather than waiting for the
12-hour schedule.

The two metrics panels ship as committed placeholder SVGs, so the profile looks finished
from the first second. They're overwritten by the real thing once step 4 is done — and if
you never do step 4, the placeholders simply stay. Nothing renders broken either way.

## 2. Turn on private contributions

Your commits **are** correctly attributed to `L33B0mb` (verified: `Lee.Dauth@gmail.com`
is linked to the account). They're just not publicly displayed, because all 19 repos are
private and GitHub hides private contributions by default.

Until this is flipped, **the streak card and the snake render empty.**

> github.com/L33B0mb → the contribution graph → **Contribution settings** ▾ → tick
> **Private contributions**

Your graph goes from a blank grid to roughly a year of real activity, shown as anonymised
daily counts. No repo names or code are exposed.

## 3. Add an avatar and fill in the profile fields

The account is still on the default identicon, and every sidebar field is blank. A great
README above a default avatar reads as a throwaway account — this is the cheapest
credibility win on the list.

> Settings → Public profile

| Field | Suggested |
|---|---|
| Profile picture | anything that isn't the identicon |
| Bio | `Building autonomous agents and local-first systems. Privacy by design.` |
| Location | `South Africa` |
| Website | `https://inunu.net` |
| Email | `brad@inunu.net` |
| Available for hire | ✅ (it's already on your `BDauth` account) |

## 4. Create the `METRICS_TOKEN` secret

The metrics panels need a classic PAT to see private-repo activity; the default
`GITHUB_TOKEN` only sees public data. Without the PAT the workflow skips those steps
cleanly and the placeholders stay.

1. Settings → Developer settings → Personal access tokens → **Tokens (classic)** →
   Generate new token
2. Scopes: **`repo`** and **`read:user`**. No expiry, or set a reminder.
3. In the `L33B0mb/L33B0mb` repo: Settings → Secrets and variables → Actions →
   New repository secret → name it **`METRICS_TOKEN`**, paste the token.
4. Actions tab → **Generate metrics** → Run workflow.

## 5. Pin your repos

Pinning only works on **public** repos — until something is public, the profile shows an
empty shelf under the README. See the recommendations below.

---

## Which repos to open — my read on all 19

I reviewed commit counts, README quality, structure and secret hygiene across the account.

### Open these

| Repo | Why | Risk check |
|---|---|---|
| **sereia** | The flagship. 64 commits, actively pushed, a genuinely excellent 25 KB README that documents capability *and* limits honestly. Clean `.gitignore` (`.env`, `data/`, vault all excluded), `.env.example` provided. This is the one that proves you build real systems. | Low — hygiene already correct |
| **yuna** | 145 commits and an unusually rigorous design corpus: 17+ specification documents, 35 numbered lifecycle invariants, formal audits, 278 passing tests. Very few portfolios show design discipline at this level. | Check `brand/` and `measurements/` for anything personal |
| **schoolfolio** | Compact, complete and finishable-looking. 18 KB README, and it demonstrates security thinking — authorization enforced in Firestore rules, explicitly called "the real trust boundary", not in the UI. | Verify Firebase config keys |

### Maybe — your call

- **lead-followup-system (Elvori)** — 39 commits, clean README, honest that the data is
  fictional. Hold back if Elvori is a live commercial product.
- **Codra-dev** — 50 commits and an interesting multi-provider agent harness, but it has
  **no README at all**. Worth opening only after writing one.

### Keep private

`anodos` (3 commits — the description promises far more than the repo contains),
`la-lia` / `lalia-web` / `Dancefit--web` (client work),
`maya-companion`, `fitcheck-ai` (2–3 commits, placeholder READMEs),
`larpadroid`, `webby` (unmodified template README),
`NY-RA` (no README), `routine-tracker`, `videos-and-marketing`,
`workspace-template`, `jarvis-workspace`, and the two forks.

### Before you flip any repo public

I could only inspect current file trees through the API, **not git history**. A file that
was committed and later deleted is still in history and still public. Run this in each
repo first:

```bash
# fast pass: anything secret-shaped anywhere in history
git log --all --name-only --format= | sort -u | grep -iE '\.env|secret|credential|\.pem$|\.key$|token|serviceaccount'

# thorough: gitleaks scans full history
gitleaks detect --source . --log-opts="--all"
```

If something turns up, it's cheaper to start a fresh repo from the current tree than to
rewrite history.

---

## Note on your second account

`BDauth` (Brad-Lee Dauth, 2012, 1,679 contributions, name/location/site/hireable already
filled in) is the stronger shell; `L33B0mb` has all the actual work. You chose `L33B0mb`,
which is the right call — work beats tenure. Worth adding a line to the `BDauth` bio
pointing at `@L33B0mb` so the older account funnels rather than competes.
