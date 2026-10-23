# Maintainer Setup Checklist

Your side of setting up the team: the GitHub fork, the tooling, and getting your friends onboarded.
Your friends' side is in [ONBOARDING.md](ONBOARDING.md) and [DAILY_WORKFLOW.md](DAILY_WORKFLOW.md).
Each section below notes the matching friend step so you can keep both docs in sync.

> **Status legend:** ✅ done · 🔲 to do · 🛠 being built (with Claude) · ⚠️ needs a decision

---

## 1. Decisions

| | Decision | Notes | Status |
|---|---|---|---|
| ⚠️ | **Hack name** | Used for the fork name and the ROM file name. Renaming a GitHub repo later is easy. | ✅ `project-poke-flora` (working name) |
| ⚠️ | **Public fork vs. private repo** | A fork of `rh-hideout/pokeemerald-expansion` is **always public**. If you want privacy, create a new private repo instead and add RHH as a remote. This checklist assumes a **fork**. | ✅ Public fork |
| ⚠️ | **Base game** | Emerald (`make`). FireRed (`make firered`) is possible but not covered here. | ✅ Emerald |
| ⚠️ | **Windows build approach** | WSL1 with the repo on the normal `C:` drive, so GitHub Desktop, Porymap and builds all use one folder. Confirm with your first Windows friend. | 🔲 |
| ⚠️ | **Main branch name** | The fork inherits `master` from RHH. Optionally rename it to `main` in GitHub settings. | 🔲 |

---

## 2. Create and configure the fork on GitHub (~10 min)

- [x] Go to <https://github.com/rh-hideout/pokeemerald-expansion> → **Fork**. *(Done 2026-10-23 with `gh repo fork`.)*
  - Name it after your hack.
  - Leaving **"Copy the master branch only"** checked is fine.
- [x] **Actions tab** → click **"I understand my workflows, go ahead and enable them."** (Actions start disabled on forks.)
  - ✅ Turned out not to be needed: Actions ran on the fork as soon as PR #1 was opened.
- [x] **Settings → General → Features** → turn on **Issues** (for tracking tasks and map ownership).
- [ ] **Settings → Collaborators** → invite each friend by GitHub username.
  - ↔ Friend step: [Onboarding §1 – Accept the GitHub invite](ONBOARDING.md#1-accept-the-github-invite)
- [x] Fork URL: <https://github.com/dabaquita/project-poke-flora>

---

## 3. Connect your local copy (with Claude) 🛠

Your local clone is at `~/dev/pokeemerald-expansion`. *(Done 2026-10-23: `origin` = your fork, `rhh` = RHH with pushes disabled, `master` tracks `origin/master`.)*

- [x] Rename the RHH remote and add your fork:
  ```bash
  git remote rename origin rhh
  ```
  ```bash
  git remote add origin https://github.com/dabaquita/project-poke-flora.git
  ```
- [x] Confirm this Mac can push to GitHub (logged in as `dabaquita`, SSH).
- [ ] Push the existing work branches (`setup/poryscript`, `docs/team-onboarding`) and open PRs **into your fork**.
  - When opening a PR, check the **base repository** is your fork, not `rh-hideout/...`.

---

## 4. Team tooling (built with Claude, reviewed by you) 🛠

Each item lands as a pull request in your fork for you to review.

| # | Piece | What it does | Status |
|---|---|---|---|
| 4.1 | **Poryscript in the build** | `make` compiles `.pory` scripts. Sample in `data/maps/OldaleTown_House1/scripts.pory`. | ✅ branch `setup/poryscript` |
| 4.2 | **GitHub Actions build + tests** | Replaces RHH's CI. Emerald only, downloads Poryscript, builds on every push/PR (**no ROM upload**: the fork is public), runs `make check` on PRs and `master`, gate job `CI passed`. Removes RHH's `docs.yml` and `labels.yml`. | 🛠 [PR #1](https://github.com/dabaquita/project-poke-flora/pull/1) |
| 4.3 | **Branch protection on `master`** | Changes only through PRs; the build must pass. (Settings → Branches.) | 🔲 |
| 4.4 | **Mac setup script** – `setup/Setup for Mac.command` | One-shot install: tools, compiler, Porymap, mGBA, VS Code, Poryscript; test build at the end. | 🔲 |
| 4.5 | **Build & Play (Mac)** – `Build & Play.command` | Double-click: `make`, then open the ROM in mGBA. Checks tools first. | 🔲 |
| 4.6 | **Windows setup** – `setup\Setup for Windows.ps1` + `setup/setup-wsl.sh` | Installs tools via winget, WSL1 Ubuntu (reboot), build packages, Poryscript. **Can't be tested on the Mac.** | 🔲 |
| 4.7 | **Build & Play (Windows)** – `Build & Play.bat` | Runs `make` inside WSL, opens the ROM in Windows mGBA. | 🔲 |
| 4.8 | **Team docs** | This file, [ONBOARDING.md](ONBOARDING.md), [DAILY_WORKFLOW.md](DAILY_WORKFLOW.md), plus planned: `EDITING_GUIDE.md`, `RULES.md`, `TROUBLESHOOTING.md`, `CREDITS.md`. | 🛠 drafts |
| 4.9 | **PR template** | Replace RHH's `.github/pull_request_template.md` with a short team one. | 🔲 |
| 4.10 | **`CODEOWNERS`** (optional) | Require your review on `src/`, `include/`, `Makefile`, `.github/`. | ⚠️ decide |

When 4.4–4.7 are done, remove the "draft" banners in the friend docs.

---

## 5. Test onboarding with friends

Run each friend through [ONBOARDING.md](ONBOARDING.md) **without helping unless they're stuck**. Every place they get stuck is a doc fix.

- [ ] **Mac friend** completes onboarding.
- [ ] **Windows friend** completes onboarding (be available: admin prompt, reboot, WSL).
- [ ] Collect screenshots from these runs for the docs (GitHub Desktop fork prompt, PR base selector, setup checklist, Porymap open-project).
- [ ] Each friend merges the **first-day exercise** PR into your fork.
- [ ] Check that **no PR showed up on `rh-hideout/pokeemerald-expansion`** (the fork PR trap).
- [ ] Update docs with everything that confused them.

| Friend | OS | Setup done | First PR merged | Notes / stuck points |
|---|---|---|---|---|
| | | 🔲 | 🔲 | |
| | | 🔲 | 🔲 | |

---

## 6. Ongoing maintainer duties

- **Review and merge PRs.** Make sure the build check is green before merging.
- **Never publish a `.gba`**: not as a CI artifact, release asset, or Discord/forum upload. The fork is public; CI must not upload ROMs. If one ever gets uploaded, delete the artifact and the run (`gh api -X DELETE repos/dabaquita/project-poke-flora/actions/artifacts/<id>`, `gh run delete <run-id>`).
- **Keep ownership current:** who is editing which maps/flags (GitHub Issues or `WHO_OWNS_WHAT.md`).
- **Keep `CREDITS.md` current** whenever assets or feature branches are added.
- **Upstream (RHH) updates**, between content milestones:
  - Early on, GitHub's **Sync fork** button works if `master` has no conflicting changes.
  - Once the hack diverges, update locally:
    ```bash
    git fetch rhh --tags
    ```
    Then merge a release tag (for example `expansion/1.17.1`) on a branch, fix conflicts, build, play-test, and open a PR.
- **Watch the memory report** at the end of each build (EWRAM/IWRAM usage) when adding C features.

---

## 7. Release builds (later: when there's a playable demo)

Not needed during early alpha. Set this up when you have something worth sharing outside the team,
for example the first town through the first gym.

**What a release build is:** `make release` builds `pokeemerald-release.gba` with `RELEASE=1`,
which turns off debug-only features (the overworld debug menu, battle debug menu, sprite visualizer).

**How hacks are distributed:** as a **`.bps` patch**, never as a `.gba`. Players apply the patch to
their own Emerald ROM. A `.gba` contains the original game's code and assets, so it must not be
posted publicly (GitHub Releases, Discord, forums).

**Planned process**
1. Freeze content on `master`, play-test, and bump the version in `CHANGELOG.md`.
2. Tag the commit: `git tag v0.1.0 && git push origin v0.1.0`.
3. A release workflow (to be added) builds `make release` on the tag, runs tests, and creates a **draft**
   GitHub Release with notes. It does **not** attach the ROM.
4. Locally: build the same tag with `make release`, then create the patch with
   [Floating IPS](https://github.com/Alcaro/Flips) against your **own dumped, clean Emerald ROM**
   (keep it outside the repo, never commit it):
   `flips --create --bps clean-emerald.gba pokeemerald-release.gba project-poke-flora-v0.1.0.bps`
5. Upload the `.bps` to the draft release, check it applies with
   [Rom Patcher JS](https://www.marcrobledo.com/RomPatcher.js/), and publish.

**Versioning:** `v0.x.y` while in development (`x` = milestone such as a new gym, `y` = fixes); `v1.0.0` for the first complete game.

---

## Reference: what's already set up on your Mac

| Thing | Where |
|---|---|
| Repo clone | `~/dev/pokeemerald-expansion` |
| Compiler (devkitARM) | `/opt/devkitpro` (env vars in `~/.zshrc`) |
| Poryscript binary | `tools/poryscript/poryscript` (gitignored) |
| Porymap | `/Applications/porymap.app` |
| mGBA | `/Applications/mGBA.app` |
| Build | `make -j$(sysctl -n hw.ncpu)` → `pokeemerald.gba` |
