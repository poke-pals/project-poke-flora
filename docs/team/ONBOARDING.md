# Onboarding: Day One

Welcome! This gets your computer ready to work on the hack. It takes **30–60 minutes**, mostly waiting for downloads.
You only do this once per computer. After today, use [DAILY_WORKFLOW.md](DAILY_WORKFLOW.md).

> **🚧 Draft:** the setup scripts and Build & Play shortcuts mentioned below are still being built.
> If a file this guide mentions doesn't exist yet, stop and message the maintainer.

**What you'll need**
- A Mac or a Windows 10/11 PC
- Your computer's password (Mac), or permission to approve admin prompts (Windows)
- A GitHub account (free: <https://github.com/signup>)

---

## What you're installing (and why)

| Tool | What it's for |
|---|---|
| **GitHub Desktop** | Downloads the project, saves your changes, and shares them with the team. No command line. |
| **Porymap** | The visual map editor: maps, NPCs, warps, wild Pokémon. |
| **VS Code** | A text editor for dialogue/scripts (`.pory`), trainer teams, and other text files. |
| **mGBA** | The Game Boy Advance emulator you test the game in. |
| **Build tools** | Turn the project files into a playable game (`pokeemerald.gba`). Installed by the setup script; you never use them directly. |

---

## 1. Accept the GitHub invite

1. Tell the maintainer your GitHub username.
2. Check your email for an invitation to join the **`poke-pals`** organization on GitHub and click **Join poke-pals**.
   (Or go to <https://github.com/orgs/poke-pals/invitation> while signed in.)

---

## 2. Install GitHub Desktop and sign in

1. Download from <https://desktop.github.com> and install it.
2. Open it and **sign in** with your GitHub account.
3. When asked for your name and email for commits, the defaults are fine.

---

## 3. Download (clone) the project

1. In GitHub Desktop: **File → Clone repository…**
2. Pick the hack's repository from the list (`poke-pals/project-poke-flora`).
3. Leave the **Local path** as the default. Click **Clone**. (It's a large download; give it a few minutes.)
4. ⚠️ **Important:** GitHub Desktop asks **"How are you planning to use this fork?"**
   Choose **"For my own purposes."**
   *Picking the other option sends your work to the wrong project.*

Your copy now lives at:
- **Mac:** `~/Documents/GitHub/project-poke-flora`
- **Windows:** `C:\Users\YOUR-NAME\Documents\GitHub\project-poke-flora`

**Tip:** In GitHub Desktop, **Repository → Show in Finder / Show in Explorer** opens this folder.

---

## 4. Run the setup script

### Mac
1. Open the project folder (see the tip above).
2. Open the `setup` folder and **double-click `Setup for Mac.command`**.
3. If macOS asks whether to open it, click **Open**.
4. Enter your **Mac password** when asked (nothing appears while you type; that's normal) and press Return.
5. Wait. At the end you'll see a checklist. Every line should have a ✅.

### Windows
1. Open the project folder (see the tip above), then the `setup` folder.
2. **Right-click `Setup for Windows.ps1` → Run with PowerShell.**
3. Click **Yes** on the admin prompt.
4. When it says to **restart your computer**, restart.
5. After restarting, **run the script again the same way**. It continues where it left off.
6. When Ubuntu opens for the first time, it asks you to make a **username and password**. Pick something you'll remember; you'll need the password later.
7. At the end you'll see a checklist. Every line should have a ✅.

**If anything shows ❌:** take a screenshot of the whole window and send it to the maintainer. Running the script again is always safe.

---

## 5. Open the project in Porymap (one time)

1. Open **Porymap**.
2. **File → Open Project…** and choose your project folder from step 3 (the one with `Makefile` in it).
   - Mac shortcut: in the file picker, press **⌘⇧G** and type `~/Documents/GitHub/project-poke-flora`.
3. If asked for a **base game version**, choose **pokeemerald**.
4. Porymap remembers this. Next time it opens straight to the project.

**Pink/magenta maps?** Maps whose names end in `_Frlg` are FireRed maps that aren't part of our game. Ignore them. Our maps don't end in `_Frlg`.

---

## 6. First-day exercise: change some dialogue

This checks that everything works, from editing to sharing.

1. **Make a branch** – GitHub Desktop: **Current Branch → New Branch**, name it `yourname-first-change`, click **Create Branch**.
2. **Edit** – In VS Code, open `data/maps/OldaleTown_House1/scripts.pory`.
   Change the text inside one of the `format("…")` lines, for example:
   `"Oh, a new TRAINER! Are you just starting out on your journey?"` → `"Hi! I'm testing the hack!"`
   Save the file.
3. **Build & Play** – Double-click **`Build & Play`** in the project folder (`.command` on Mac, `.bat` on Windows).
   mGBA opens with the game.
4. **Find your change** – Walk to **Oldale Town** (north of Route 101) and talk to the woman in the **bottom-left house**.
   - To skip ahead: hold **S** and press **Return** (Mac) / **Enter** (Windows) in the overworld to open the debug menu → **Utilities → Warp**.
5. **Commit** – Back in GitHub Desktop, you'll see `scripts.pory` in the changed files list. Type a summary like `Test dialogue change` and click **Commit to yourname-first-change**.
6. **Push** – Click **Publish branch**.
7. **Pull request** – Click **Create Pull Request**. A browser page opens.
   ⚠️ Check that **base repository** shows **`poke-pals/project-poke-flora`**, **not** `rh-hideout/pokeemerald-expansion`. Then click **Create pull request**.
8. Tell the maintainer. Once they merge it, you're officially set up! 🎉

---

## One rule to know from day one

**Never share the game file (`.gba`).**
- Don't post `pokeemerald.gba` anywhere public (Discord servers, forums, file-sharing links), and don't send it to people outside the team.
- A built `.gba` contains the original Pokémon Emerald, so sharing it is sharing Nintendo's game. Everyone on the team builds their own copy with Build & Play.
- Show progress with **screenshots or videos** instead. Public releases will be **`.bps` patches** only, made by the maintainer.
- Git already ignores `.gba` files, so GitHub Desktop never lists them. Don't rename or move one to get around that.

More rules are in [DAILY_WORKFLOW.md](DAILY_WORKFLOW.md#3-make-your-changes).

---

## mGBA controls (default)

| GBA button | Mac | Windows |
|---|---|---|
| D-pad | Arrow keys | Arrow keys |
| A / B | X / Z | X / Z |
| L / R | A / S | A / S |
| Start / Select | Return / Delete | Enter / Backspace |
| Fast forward (hold) | Tab | Tab |
| Save state 1–9 | Shift + F1–F9 (add **fn** on most Macs) | Shift + F1–F9 |
| Load state 1–9 | F1–F9 (add **fn**) | F1–F9 |
| Reset game | ⌘R | Ctrl+R |

Change keys in **Settings → Controllers** (Mac: **mGBA → Settings**; Windows: **Tools → Settings**).

---

## Next

- Everyday steps: [DAILY_WORKFLOW.md](DAILY_WORKFLOW.md)
- Stuck? Screenshot it and message the maintainer.
