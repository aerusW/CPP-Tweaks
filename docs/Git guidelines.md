# Git Guidelines — cpp-tweaks
A playground repo for tests, experiments, and random C++ things. Loose on what goes in, strict on one thing: main stays clean and nobody breaks it for everyone else.

## The golden rule
Never commit or push directly to main. Every experiment, test, or change lives on its own branch and reaches main through a Pull Request. main should always build and run — it's the one shared thing everyone pulls from.

## Branch workflow
Everything you do gets its own branch, created off the latest main.

### Branch naming
This repo is shared and full of unrelated experiments, so put your name first — it's instantly obvious whose branch is whose — then a short description:
`<yourname>/<short-description>`

> Examples: francesco/raylib-test, marco/sorting-benchmark, francesco/pointer-experiments

If you prefer typed prefixes, these are fine too: test/, experiment/, fix/, wip/. The only hard rule: descriptive, lowercase, hyphenated, no spaces.
Step by step

1. Switch to main and pull the latest.
2. Create your branch off it.
3. Work. Commit as you go.
4. Push the branch (Publish Branch the first time).
5. Open a Pull Request on GitHub.
6. Merge it (after review if you turned that on). Delete the branch.

 
## Committing
 
This is a playground, so commit discipline is relaxed **on your own branch** — commit early, commit often, save progress however you like. `wip:` commits are completely fine here.
 
The one thing that still matters: **when you open a PR to `main`, the branch should at least build.** Messy history on your branch is fine; a broken `main` is not.
 
### Commit message format (loose)
 
A short line describing what changed is enough:
 
```
add raylib window test
fix segfault in vector loop
wip: trying a constexpr approach
```
 
Imperative tense ("add", not "added") if you want consistency, but nobody's enforcing it here.
 
## Pulling and pushing
 
- **Pull `main`** whenever you sit down to work, *before* creating a new branch — keeps you current and avoids conflicts.
- **Push your branch** at the end of a session so your work is backed up and your friends can see it. First push: click **Publish Branch**.
- If GitHub says your branch is behind `main`, update it (see Common situations).
 
## Pull Requests
 
A PR is how your branch gets into `main`.
 
- Open one when your experiment is ready — or a **Draft PR** for early feedback on unfinished work.
- **Reviewing** (if enabled): glance at the **Files changed** tab, comment if something's off, approve.
- For solo experiments with review turned off, just merge your own PR — the PR still gives you a record and, crucially, keeps direct pushes off `main`.
- **After merging: delete the branch.** GitHub offers a button right there. Then everyone pulls `main` before starting new work.
 
## C++ housekeeping: don't commit build junk
 
A C++ repo fills up with compiled output fast. Add a `.gitignore` at the repo root so binaries and build folders never get committed:
 
```gitignore
# Build output
/build/
*.o
*.obj
*.exe
*.out
a.out
 
# IDE / editor
.vscode/
*.user
 
# OS
.DS_Store
Thumbs.db
```
 
Commit the **source** (`.cpp`, `.h`/`.hpp`, `CMakeLists.txt`), never the compiled results. If you already committed a binary by accident, `git rm --cached <file>` removes it from the repo while keeping your local copy.
 
## Common situations
 
### "`main` moved on and my branch is behind"
 
In VSCode:
1. Switch to `main`, pull.
2. Switch back to your branch.
3. Source Control → **...** → **Branch** → **Merge Branch...** → pick `main`.
### "I have a merge conflict"
 
VSCode marks the conflicting files. Open them, click **Open in merge editor** (bottom-right), pick what to keep, save, stage the file, commit. If you're unsure, ask whoever wrote the other side before resolving.
 
### "I tried to push to `main` and it got rejected"
 
That's the protection working as intended. Move your commits onto a branch:
1. Create a new branch from your current state (your commits come with you).
2. Push that branch and open a PR.
If you'd already committed locally on `main`, make a branch from it first, then reset your local `main` back to match GitHub — ask in the group chat if you're not sure. **Don't force-push.**
 
## Quick reference
 
| Situation | Action |
|---|---|
| Starting work | Pull `main`, create a `yourname/thing` branch |
| Made progress | Commit (`wip:` is fine on your own branch) |
| End of session | Push your branch |
| Ready to share | Open a PR (Draft for early feedback) |
| PR looks good | Merge on GitHub, delete the branch |
| Starting next task | Pull `main` again |
| Touching `main` directly | Don't — that's what the protection blocks |