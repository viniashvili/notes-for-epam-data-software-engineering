# Version Control With Git

### **Version Control System (VCS)**

**Definition:**
A system that tracks and manages changes to files (usually code) over time.

**Key Concepts:**

1. **Tracking Changes** – Records every change as a version/commit.
2. **Collaboration** – Multiple people can work on the same project safely.
3. **Backup & Restore** – Revert to previous versions if needed.
4. **Branching & Merging** –

   * Branch: work on new features/experiments separately.
   * Merge: combine changes back into main code.

**Types:**

* **Centralized VCS (CVCS):** Single central repository (e.g., SVN).
* **Distributed VCS (DVCS):** Each user has a full repository copy (e.g., Git).

**Example:** Like writing a book with friends where edits are tracked, and you can restore previous drafts.

---

### **Version Control Types**

1. **Centralized Version Control System (CVCS)**

   * Uses a **single central repository**.
   * All users **check out and commit changes** to the central server.
   * **Pros:** Simple, easy to understand, single source of truth.
   * **Cons:** Single point of failure; needs network access.
   * **Examples:** SVN, CVS, Perforce.

2. **Distributed Version Control System (DVCS)**

   * Every user has a **full copy of the repository** (history + code).
   * Changes are committed **locally** and then **pushed/pulled** to/from others.
   * **Pros:** Can work offline; no single point of failure; easy branching/merging.
   * **Cons:** Slightly more complex; larger storage.
   * **Examples:** Git, Mercurial, Bazaar.

---

### **Why Git?**

**Git** is a **Distributed Version Control System (DVCS)** widely used because it offers:

1. **Distributed Architecture**

   * Every user has a full copy of the repository.
   * Work offline, commit locally, and sync later.

2. **Speed & Performance**

   * Operations like commit, branch, and merge are **very fast** because they are local.

3. **Reliable & Safe**

   * Complete history is stored locally → reduces risk of data loss.

4. **Powerful Branching & Merging**

   * Easy to create branches for features, experiments, or fixes.
   * Merge changes safely with minimal conflicts.

5. **Collaboration Friendly**

   * Multiple developers can work simultaneously without overwriting each other’s work.

6. **Widely Used & Supported**

   * Git integrates with platforms like **GitHub, GitLab, Bitbucket**.
   * Huge community and plenty of tutorials/tools available.

---

### **.git Folder Structure**

The `.git` folder is created when you run `git init` and contains all metadata and history for the repository.

**Key components:**

1. **HEAD**

   * Points to the **current branch** reference (which commit you are on).

2. **config**

   * Repository-specific Git **configuration settings**.

3. **description**

   * Used mainly by **Git web interfaces** (not crucial for normal Git use).

4. **hooks/**

   * Contains **scripts** that run on certain Git events (pre-commit, post-commit, etc.).

5. **info/**

   * Contains **excludes** file for patterns to ignore (like `.gitignore`, but local).

6. **objects/**

   * Stores **all the content (blobs, trees, commits)** in compressed form.
   * Git database of all history.

7. **refs/**

   * Stores references to **branches, tags, and remotes**.
   * Subfolders: `heads/` (local branches), `tags/` (tags), `remotes/` (remote branches).

8. **logs/**

   * Keeps a **record of changes** to refs (useful for recovering lost commits).

9. **index**

   * The **staging area**, stores info about what will go into the next commit.

---

### **Undoing Changes in Git**

1. **`git status`**

   * Check current changes (staged, unstaged, untracked).

2. **Discarding Changes in Working Directory**

   * **Unstaged changes:**

     ```bash
     git checkout -- <file>    # Restore file to last committed state
     ```
   * **Staged changes:**

     ```bash
     git reset <file>          # Unstage file
     ```

3. **`git reset`**

   * Moves **HEAD** to a previous commit.
   * **Soft reset:**

     ```bash
     git reset --soft <commit>
     ```

     → Keeps changes in staging area.
   * **Mixed reset (default):**

     ```bash
     git reset <commit>
     ```

     → Keeps changes in working directory but unstages them.
   * **Hard reset:**

     ```bash
     git reset --hard <commit>
     ```

     → Discards all changes in working directory and staging area.

4. **`git revert`**

   * Creates a **new commit that undoes a previous commit**.
   * Safe for **public/shared branches**.

     ```bash
     git revert <commit>
     ```

---

### **.gitignore**

* A file that **tells Git which files/folders to ignore**.
* Prevents committing **temporary files, build artifacts, logs, secrets**.
* Example:

  ```
  *.log
  __pycache__/
  .env
  ```

---

### **Git Branching & Merging**

1. **Branching**

   * Create separate lines of development.
   * **Commands:**

     ```bash
     git branch <branch_name>    # Create a branch
     git checkout <branch_name>  # Switch to branch
     git switch <branch_name>    # Alternative to checkout
     git checkout -b <branch_name>  # Create + switch
     ```

2. **Merging**

   * Combine changes from one branch into another.
   * **Command:**

     ```bash
     git merge <branch_name>
     ```
   * **Fast-forward merge:** No divergent commits; just moves HEAD.
   * **3-way merge:** Branches diverged; Git combines changes.

3. **Conflict Solving**

   * Happens when **same lines changed in different branches**.
   * Resolve manually in files, then:

     ```bash
     git add <file>    # Mark conflict resolved
     git commit        # Complete merge
     ```

---

### **Other Useful Commands**

1. **Rebase**

   * Moves or reapplies commits **on top of another base branch**.
   * **Command:**

     ```bash
     git rebase <branch_name>
     ```
   * Pros: Cleaner, linear history.
   * Cons: Can rewrite history → avoid on shared branches.

2. **Cherry-pick**

   * Apply **specific commit(s) from another branch**.
   * **Command:**

     ```bash
     git cherry-pick <commit_hash>
     ```

---

### **Git Tags**

**Definition:**

* A tag is a **reference to a specific commit**.
* Used to mark **important points** in history, like **releases or versions**.

**Types of Tags:**

1. **Lightweight Tag**

   * Simple pointer to a commit.
   * Like a **bookmark**.
   * **Command:**

     ```bash
     git tag <tag_name>
     ```

2. **Annotated Tag**

   * Stored as a full object in Git.
   * Contains **tagger name, date, message, and signature**.
   * Recommended for releases.
   * **Command:**

     ```bash
     git tag -a <tag_name> -m "message"
     ```

**Viewing Tags:**

```bash
git tag           # List all tags
git show <tag>    # Show tag details
```

**Pushing Tags to Remote:**

```bash
git push origin <tag_name>
git push --tags   # Push all tags
```

**Use Case:**

* Marking **v1.0, v2.0** releases in a project for easy reference.

---

### **Git Stashing**

**Definition:**

* **Temporarily saves** changes in your working directory that are not ready to commit.
* Allows you to **switch branches or work on something else** without losing your changes.

**Key Commands:**

1. **Stash changes:**

```bash
git stash
```

* Saves **unstaged and staged changes**.
* Restores working directory to **last commit state**.

2. **List stashes:**

```bash
git stash list
```

3. **Apply stash:**

```bash
git stash apply       # Apply latest stash without removing it
git stash apply stash@{2}  # Apply specific stash
```

4. **Pop stash:**

```bash
git stash pop         # Apply and remove stash from list
```

5. **Drop stash:**

```bash
git stash drop stash@{0}  # Delete specific stash
```

**Use Case:**

* You’re in the middle of work, but need to **switch branch for a quick fix**. Stash your changes, switch branches, then reapply them later.

---

### **Git Remotes**

**Definition:**

* A **remote** is a **version of your repository stored on a server** (like GitHub, GitLab, or Bitbucket).
* Allows **collaboration** and **sharing code** with others.

**Key Concepts & Commands:**

1. **View remotes:**

```bash
git remote -v
```

* Shows **remote names** and URLs.

2. **Add a remote:**

```bash
git remote add <name> <url>
```

* Example:

```bash
git remote add origin https://github.com/user/repo.git
```

3. **Rename a remote:**

```bash
git remote rename <old_name> <new_name>
```

4. **Remove a remote:**

```bash
git remote remove <name>
```

5. **Fetch from remote:**

```bash
git fetch <remote_name>
```

* Updates your **local copy of remote branches** without merging.

6. **Push to remote:**

```bash
git push <remote_name> <branch_name>
```

7. **Pull from remote:**

```bash
git pull <remote_name> <branch_name>
```

* Fetches and merges remote changes into your local branch.

**Use Case:**

* Collaboration: Team members **push** their commits to the remote and **pull** others’ changes.
* Backup: Remote acts as a **central copy** of your repository.

---

### **Git Branching Strategies**

1. **Main / Master Branching**

   * Single main branch (`main` or `master`) holds **production-ready code**.
   * All changes are merged here after testing.

2. **Feature Branching**

   * Create a **branch for each new feature**.
   * **Command:**

     ```bash
     git checkout -b feature/<feature_name>
     ```
   * Merge back to `main` after completion.

3. **Git Flow**

   * Popular strategy for **release management**.
   * Branches:

     * `main` / `master` → production
     * `develop` → integration of features
     * `feature/*` → new features
     * `release/*` → pre-release stabilization
     * `hotfix/*` → urgent fixes to production

4. **GitHub Flow**

   * Simplified flow, mostly used for **continuous deployment**.
   * Only `main` branch exists as production.
   * Features are developed in branches and merged via **Pull Requests**.

5. **GitLab Flow**

   * Combines **Git Flow** and **issue tracking**.
   * Branches based on **environments** (production, staging, testing).
   * Supports **continuous integration** pipelines.

6. **Trunk-Based Development**

   * All developers **commit small changes directly to main/trunk** frequently.
   * Uses **short-lived feature branches** if needed.
   * Focus on **continuous integration & delivery**.

**Use Cases:**

* Choose strategy based on **team size, release frequency, and deployment style**.
* Large teams often use **Git Flow**; small/fast-moving teams often prefer **GitHub Flow**.

---

