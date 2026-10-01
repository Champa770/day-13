## Branching & Merging

**What a branch is**

A branch is an independent line of development — a separate copy of your project's history where you can make changes without affecting the main codebase. Think of it as a parallel timeline that can later be merged back in, or discarded if the experiment didn't work out.

**The default branch**

```bash
git branch
```

Shows all branches, with a `*` next to the one you're currently on. Every new repo starts with one branch — usually `main` (older projects sometimes use `master`).

**Why branch instead of just editing `main` directly**If you build a new feature directly on `main` and it breaks something, your main codebase is broken. Branching lets you build and test in isolation, and only merge into `main` once it actually works.

**Creating a branch**

```bash
git branch feature-navbar
```

This creates the branch but doesn't switch to it — you're still on whichever branch you were on before.

**Switching branches**

```bash
git checkout feature-navbar
```

or the newer command (functionally similar, introduced to make branch operations less confusing):

```bash

``````bash
git switch feature-navbar
```

**Create and switch in one step**

```bash
git checkout -b feature-navbar
```

or

```bash
git switch -c feature-navbar
```

- `b` / `c` = create the branch and move onto it immediately. This is the version used constantly in real workflows.

**Working on a branch**

Once switched, everything behaves normally — edit files, `git add`, `git commit` — except these commits only exist on `feature-navbar`, not on `main`, until merged.

```bash
git switch -c feature-navbar

```**Switching back**

```bash
git switch main
```

Your files in the working directory actually change to match whatever `main` looked like — the navbar changes are still safe on `feature-navbar`, just not visible here.

**Merging — bringing a branch's changes into another**

```bash
git switch main
git merge feature-navbar
```

This takes all commits made on `feature-navbar` and applies them onto `main`. Always switch to the branch you want to receive the changes *before* running `merge`.

**Fast-forward merge**

If `main` hasn't changed at all since the branch was created, Git just moves `main`'s pointer forward — no real "merging" logic needed, just a straight-line history.**Merge conflicts — when Git needs help**

If both branches changed the *same lines* of the *same file*, Git can't automatically decide which version is correct. It pauses the merge and marks the conflict directly in the file:

```
<<<<<<< HEAD
<h1>Welcome to my site</h1>
=======
<h1>Welcome to my awesome site</h1>
>>>>>>> feature-navbar
```

- `HEAD` side = current branch's version (the one you merged into)
- Bottom side = the incoming branch's version

You manually edit the file to keep the correct content, delete the `<<<<<<<`, `=======`, `>>>>>>>` markers, then:

```bash
git add .

``````bash
git commit -m "Resolve merge conflict in navbar heading"
```

The commit here finalizes the merge — Git treats a resolved conflict as a special commit with two parent commits.

**Deleting a branch (after merging, to clean up)**

```bash
git branch -d feature-navbar
```

- `d` only deletes if it's already been merged (safe). Force-delete an unmerged branch with `D` — rarely needed, and risky if the work isn't saved elsewhere.

**Common mistakes**

- Forgetting which branch you're on before making changes (`git branch` or `git status` shows this — check often)
- Panicking during a merge conflict instead of just reading the file and choosing the right content
- Deleting a branch before merging it, losing that work
- Trying to merge from the wrong direction (merging `main` into the feature branch, then confusing yourself about which one is "ahead")

**Small practice task****Small practice task**

- On yesterday's repo, create a branch called `feature-about-page`
- Switch to it, create an `about.html` file, commit it
- Switch back to `main`, confirm `about.html` doesn't exist there
- Merge `feature-about-page` into `main`
- Confirm `about.html` now appears on `main`
- Deliberately edit the same line of the same file differently on two branches, merge them, and practice resolving the conflict manually# day-13
git 2
