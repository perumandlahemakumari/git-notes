
# 🧠 Git Branching Example: `main` and `dev`

This repo explains the difference between `git merge`, `git rebase`, and `git cherry-pick` using simple examples.

---

## 📁 Initial Setup

```bash
git init demo-repo
cd demo-repo
echo "First Commit" > file.txt
git add .
git commit -m "Initial commit on main"
```

Create a `dev` branch from `main`:

```bash
git checkout -b dev
```

---

## 📌 Commits on `main`

```bash
git checkout main
echo "Main Commit 1" >> file.txt
git commit -am "Main: Commit 1"
echo "Main Commit 2" >> file.txt
git commit -am "Main: Commit 2"
```

## 📌 Commits on `dev`

```bash
git checkout dev
echo "Dev Commit A" >> file.txt
git commit -am "Dev: Commit A"
echo "Dev Commit B" >> file.txt
git commit -am "Dev: Commit B"
```

At this point:

```
main:      C1 -- C2
               \
dev:             A -- B
```

---

## 🔁 1. `git merge`

```bash
git checkout main
git merge dev
```

**Result:** Creates a merge commit combining histories.

```
main: C1 -- C2 ------ M
                     / \
             A ---- B   (merge commit M)
```

✅ Full history retained  
❌ Can clutter history

---

## 🔄 2. `git rebase`

Reset for clean rebase:

```bash
git checkout main
git reset --hard HEAD~3
echo "Main Commit 1" >> file.txt
git commit -am "Main: Commit 1"
echo "Main Commit 2" >> file.txt
git commit -am "Main: Commit 2"

git checkout dev
echo "Dev Commit A" >> file.txt
git commit -am "Dev: Commit A"
echo "Dev Commit B" >> file.txt
git commit -am "Dev: Commit B"
```

Now rebase:

```bash
git checkout dev
git rebase main
```

**Result:** Replays `dev` commits on top of `main`

```
main: C1 -- C2
                \
dev:             A' -- B'
```

✅ Clean, linear history  
❌ Do not use on shared branches

---

## 🍒 3. `git cherry-pick`

To pick only **Dev Commit B** to `main`:

```bash
git checkout dev
git log --oneline   # Copy commit hash of B (e.g., abc123)

git checkout main
git cherry-pick abc123
```

```
main: C1 -- C2 -- B
dev:             A -- B
```

✅ Pick only what’s needed  
❌ Can lead to duplication/conflicts

---

## ✅ Summary Table

| Command           | Purpose                         | Keeps History | Rewrites History | Use Case                        |
|------------------|----------------------------------|----------------|------------------|---------------------------------|
| `git merge`       | Combine changes with history     | ✅ Yes         | ❌ No            | Safe, collaborative merges      |
| `git rebase`      | Replay changes on another base   | ❌ No          | ✅ Yes           | Clean, linear history           |
| `git cherry-pick` | Apply specific commits           | ✅ Yes         | ❌ No            | Hotfixes or selective features  |

---

> Created for Git learning purpose – suitable for GitHub README or LinkedIn Post 📘
