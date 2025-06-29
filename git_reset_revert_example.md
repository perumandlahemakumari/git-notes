
# 🔁 Git `revert` vs `reset` (soft, mixed, hard)

This guide explains the **difference between `git revert` and `git reset`** using examples. We'll cover:

- `git revert`
- `git reset --soft`
- `git reset --mixed`
- `git reset --hard`

---

## 🎯 Setup Example

```bash
git init reset-repo
cd reset-repo
echo "Line 1" > file.txt
git add .
git commit -m "Commit 1: Initial"

echo "Line 2" >> file.txt
git add .
git commit -m "Commit 2: Add Line 2"

echo "Line 3" >> file.txt
git add .
git commit -m "Commit 3: Add Line 3"
```

History:
```
C1 -- C2 -- C3 (HEAD)
```

---

## 1️⃣ `git revert`

```bash
git revert HEAD
```

- Reverts the **last commit (C3)** by creating a new commit that undoes its changes.
- Safe for shared branches.

**Resulting history:**
```
C1 -- C2 -- C3 -- C4 (C4 is the revert of C3)
```

✅ Adds a new commit  
✅ Keeps history intact  
✅ Safe on public branches

---

## 2️⃣ `git reset --soft`

```bash
git reset --soft HEAD~1
```

- Moves HEAD back to C2  
- Keeps all changes in the **staging area (index)**

**Resulting state:**
```
C1 -- C2 (HEAD)
         (Changes from C3 are staged)
```

✅ Use to rewrite history before pushing  
✅ Good for combining commits

---

## 3️⃣ `git reset --mixed` (default)

```bash
git reset --mixed HEAD~1
```

- Moves HEAD back to C2  
- Keeps changes in the **working directory**, but not staged

**Resulting state:**
```
C1 -- C2 (HEAD)
         (Changes from C3 are unstaged)
```

✅ Useful to unstage files  
⚠️ Not safe on pushed/shared commits

---

## 4️⃣ `git reset --hard`

```bash
git reset --hard HEAD~1
```

- Moves HEAD back to C2  
- **Deletes all changes** from working directory and staging area

**Resulting state:**
```
C1 -- C2 (HEAD)
         (No changes from C3 remain)
```

⚠️ Irreversible (unless you use `git reflog`)  
⚠️ DANGEROUS if used carelessly

---

## 📌 Summary Table

| Command                 | Changes Commit History | Keeps Changes | Keeps in Index | Use Case                          |
|------------------------|------------------------|----------------|----------------|-----------------------------------|
| `git revert <commit>`  | ❌ No                  | ✅ Yes        | ✅ Yes        | Undo specific commits safely     |
| `git reset --soft`     | ✅ Yes                 | ✅ Yes        | ✅ Yes        | Undo commits but keep staging    |
| `git reset --mixed`    | ✅ Yes                 | ✅ Yes        | ❌ No         | Unstage files without deleting   |
| `git reset --hard`     | ✅ Yes                 | ❌ No         | ❌ No         | Completely reset (DANGEROUS)     |

---

> Use `git reflog` to recover if you accidentally reset important commits.
