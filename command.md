| Command | What It Does |
|---------|--------------|
| ```git init``` | Turns your folder into a Git repository |
| ```git clone <repo-url>``` | Downloads a remote GitHub repo to your PC |
| ```git status``` | Shows changed, staged, and untracked files |
| ```git add <file>``` | Stages a specific file |
| ```git add .``` | Stages all files in current folder |
| ```git commit -m "message"``` | Creates a commit with a message |
| ```git log``` | Shows commit history |
| ```git branch``` | Lists all branches |
| ```git branch new``` | Creates a new branch named *new* |
| ```git checkout new``` | Switches to branch *new* |
| ```git merge new``` | Merges branch *new* into current branch |
| ```git branch -d new``` | Deletes branch *new* |
| ```git diff``` | Shows changes not yet staged |
| ```git diff "Array .java"``` | Shows diff of file with space in name |
| ```git reset --hard HEAD``` | Removes all uncommitted changes |
| ```git reset --hard HEAD^``` | Moves branch to previous commit |
| ```git restore <file>``` | Discards changes of a specific file |
| ```git restore .``` | Discards all changes in working directory |
| ```git push``` | Uploads your commits to GitHub |
| ```git pull``` | Downloads + merges changes from GitHub |
| ```git remote -v``` | Shows remote repo URL(s) |
| ```git add "Array .java"``` | Adds file with spaces |
| ```HEAD``` | Shows the current branch pointer |

=================================================================================================================

🟦 Before creating a new branch (only main exists)
main is pointing to C3:
Here is why:
A branch always points to the latest commit in its history.
Since the commits go from C1 → C2 → C3, the latest one is C3.
HEAD is pointing to main, so ultimately HEAD → main → C3.
✅ HEAD usually points to the current branch name (not directly to a commit)

In normal situations:  HEAD → main → C3
HEAD points to the branch
The branch points to the commit
So HEAD indirectly points to the commit, but through the branch.

main
 ↓
[C1] → [C2] → [C3]
              ↑
             HEAD

/* 
✅ When does HEAD not point to a branch?

There is one special case:  Detached HEAD state
If you checkout a specific commit:   git checkout C2
Then:
HEAD → C2   (directly to the commit)
Not to a branch.
*/


🟩 After: git branch new_branch
What happened?
A new pointer new is created
It points to the same commit as main (C3)
No file copied
No commit copied
Branch = just a name pointing to a commit

main        new_branch
 ↓           ↓
[C1] → [C2] → [C3]
              ↑
             HEAD


🟧 After switching to new: git checkout new
main        new
 ↓           ↓
[C1] → [C2] → [C3]
              ↑
             HEAD


Only HEAD moves to point to new
Your files remain same (since both branches point to C3)


🟨 After making a new commit on new branch
main
 ↓
[C1] → [C2] → [C3]

                      HEAD
                       ↓
                     new
                      ↓
                    [C4]
Now:
main still points to C3
new moved ahead to C4
HEAD follows the branch you are on (new)

| Item             | Meaning                                 |
| ---------------- | ----------------------------------------|
| Commit           | A node linked to the previous commit    |      👉actual data (snapshot)
| Branch(main)     | A pointer to a commit                   |      👉just a label pointing to latest commit
| HEAD             | Points to the current branch(or current commit)|👉tells “where you are currently working”
| `git branch x`   | Creates a pointer at the current commit |
| `git checkout x` | Moves HEAD to that branch               |
| New commit       | Moves only the current branch pointer   |

🧠 Interpretation
C = latest commit
branch(main) = pointer to C
HEAD = tells “you are on main branch”

👉What happens when you commit?
New commit D is created:
A ← B ← C ← D
            ↑
          main
            ↑
           HEAD
👉 Only main moves forward
👉 HEAD follows automatically

==================================================================================================================

✅⭐ 1. What is git init ?
Command: git init, Turns your folder into a Git repository.

What happens internally:
Git creates a hidden folder named .git inside your project.

This folder stores:
all commits
branches
your Git history
staging area

Your project becomes a Git Repository.
👉 Before git init: your folder = normal folder
👉 After git init: your folder = version-controlled folder

================================================================================================================

✅⭐ 2. What is git clone ?
Command:
git clone <repo-url>
git clone <url> myfolder_name
What happens internally:
Download a remote repository to your local system(all branches + commits)
Creates a new folder with the project contents
Automatically sets origin as the remote (GitHub link)
This is used when working on existing GitHub projects.

✅Example:
git clone https://github.com/user/project.git

===================================================================================================================

✅🚀 1. What is git fetch ?
git fetch is used to: Download latest commit(changes) from remote WITHOUT Merge them into your current branch.
🔥Basic Syntax:
git fetch
👉 OR:
git fetch origin


🌳Before git fetch
Remote:
A ← B ← C ← D   (origin/main)
Local:
A ← B ← C       (main)
        ↑
       HEAD
👉 You are behind

🔥After git fetch
Remote tracking updated:
A ← B ← C ← D   (origin/main)

Local unchanged:
A ← B ← C       (main)
        ↑
       HEAD

==================================================================================================================

✅🚀 1. What is git pull?
git pull is used to: fetch latest commits(changes) from remote repo AND Merge them into your current branch
It does 2 operations together: git pull = git fetch + git merge

🔥Basic Syntax: git pull
👉 OR explicitly: git pull origin main


🌳 3. Before git pull (Important Diagram)
Remote repo:
A ← B ← C       (main)
        ↑
       HEAD

🔥After git pull
A ← B ← C ← D
            ↑
          main
            ↑
           HEAD

🔥git fetch vs git pull          
| Command     | Action           |
| ----------- | ---------------- |
| `git fetch` | Download only    |
| `git pull`  | Download + merge |

git push : Uploads commits to GitHub.
git pull: Downloads latest commits from GitHub.
====================================================================================================================

✅⭐ 3. What is git status ?
git status shows: Current state of your working directory and staging area
Shows:
What files changed?
What is staged?
What is not staged?
Which branch am I on ?

Git divides files into 3 areas:
| Area                     | Meaning               |
| ---------------------    | --------------------- |
| 1. **Working directory** | Your actual files     |
| 2. **Staging area**      | Files ready to commit |
| 3. **Repository**        | Saved commits         |

🔥 Full Command Flow:
[Your Code Changes]
        ↓
Working Directory
        ↓ (git add)
Staging Area
        ↓ (git commit)
Local Repository (permanent)
        ↓ (git push)
Remote Repository (GitHub)

//=============================================================================================================

✅⭐ 4. What is git add ?
Command:  git add file.java

git add file.java moves file.java from:
👉 Working Directory → Staging Area
This means the file is now prepared for the next commit.
Staging area = "final preparation room" before commit.

===================================================================================================================

✅⭐ 5. What is git commit ?
Command:  git commit -m "message"
moves code changes from the Staging Area → to the Permanent Repository.
Working Directory  →  Staging Area  →  Repository (Permanent)
        (git add)      (git commit) 

git commit saves all staged changes permanently into Git history.

What happens internally:
Git takes snapshots of all staged files in the staging area
Creates a commit object
Each commit has:
    author name
    date
    commit message
    pointer to previous commit
   unique hash ID (like a63b1c8)
Commit = Perfect backup of code at that moment.
| Command                              | Example Output              | Meaning                                    |
| ------------------------------------ | --------------------------- | ------------------------------------------ |
| `git commit`                         | Opens editor                | Create commit (manual message writing)     |
| `git commit -m "msg"`                | `[main abc123] msg`         | Commit with message directly               |
| `git commit -am "msg"`               | `[main abc123] msg`         | Add + commit (only tracked files)          |
| `git commit --amend`                 | `[main def456] updated msg` | Modify last commit (message/files)         |
| `git commit --amend -m "new msg"`    | `[main def456] new msg`     | Change last commit message                 |
| `git commit --no-edit --amend`       | `[main def456]`             | Add changes to last commit (no msg change) |
| `git commit -v`                      | Shows diff + editor         | See changes while writing commit           |
| `git commit --author="Name <email>"` | `[main abc123] msg`         | Override author                            |
| `git commit --date="2024-01-01"`     | `[main abc123] msg`         | Set custom date                            |
| `git commit -a`                      | Opens editor                | Auto-stage tracked files + commit          |

===================================================================================================================

✅⭐ 6. What is git log ?
Command:  git log = show me history of commits.
git log is a command used to show the history of commits in your Git repository.

Think of it like a timeline that shows:
Who made the commit
When the commit was made
The commit message
The unique commit ID (SHA-1 hash)
It helps you track changes, debug issues, and understand project progress.

| Command                    | Meaning                               |
| -------------------------- | ------------------------------------- |
| `git log`                  | Full detailed commit history          |
| `git log --oneline`        | Shows commits in one short line       |
| `git log --graph`          | Shows branch structure as ASCII graph |
| `git log --decorate`       | Shows branch & tag names              |
| `git log --author="Kapil"` | Filter commits by author              |
| `git log -p`               | Show changes made in each commit      |


====================================================================================================================

✅⭐ 7. What is a Branch ?
Think of Branch like:
A separate copy of code, made for working safely without touching main.
👉 Commits = actual data (snapshots)
👉 Branch = pointer (label) to a commit

What happens internally:
Branch is just a pointer to a commit
main points to last commit
new-feature can point to another commit


🚀 Basic Command
git branch
Output:
* main
  feature
  dev
| Output    | Meaning                                |
| --------- | -------------------------------------- |
| `* main`  | ⭐ You are currently on **main branch** |
| `feature` | Another branch exists                  |
| `dev`     | Another branch exists                  |
🔥 Key Rule
👉 * (star) = current active branch (HEAD is here)


| Command                         | Meaning                            |                 
| ------------------------------- | ---------------------------------- |
| `git branch`                    | Shows **all branches** in the repo |
| 'git branch | grep branch_Name  |Show only a specific branch_name    |
|  git branch -v branchName       | Display detailed info about a single branch |

Creating branch:
| `git branch branchName`         | Creates a **new branchName**       |
| `git branch -d branchName`      | Deletes a branch (safe delete)     |
| `git branch -D branchName`      | Force delete branch                |
| `git branch -m newName`         | Rename current branch              |
| `git branch -m oldName newName` | Rename any branch                  |

What happens:
Git creates a pointer named branchName
Points to the same commit where you currently are
No new files created
No copying
===================================================================================================================

✅⭐ 9. git checkout

Switch branch: git checkout new_branch

What happens internally:
Git changes your working directory files
It replaces them with the version stored in that branch
HEAD now points to the new_branch branch

HEAD = the branch you are currently on.

| 🟩 **Command**                           | 🟦 **Meaning / What It Does**                                   |
| ---------------------------------------- | ---------------------------------------------------------------- |
| `git checkout branchName`                | Switch to an existing branch                                     |
| `git checkout -b newBranch`              | Create a new branch **and** switch to it                         |
| `git checkout -`                         | Go back to **previous** branch                                   |
| `git checkout branchName -- fileName`    | Bring **only that file** from another branch into current branch |
| `git checkout -- fileName`               | Discard changes → Restore file to last committed version         |
| `git checkout -t origin/branchName`      | Checkout a **remote branch** and start tracking it               |
| `git checkout -b newBranch <commitHash>` | Create a new branch starting from an **older commit**            |
| `git checkout <commitHash>`              | Checkout a **specific commit** → Detached HEAD mode              |

===================================================================================================================

✅⭐ 10. git merge
git merge is used to: Combine changes from one branch into another
🧠 Simple Meaning:   Take code from one branch and bring it into your current branch

🔥 Basic Syntax:
git merge <branch_name>

🔥 Example:
git checkout main
git merge feature
👉 Meaning: Merge feature branch into main


🧠 Meaning of below diagrams:
A → B → C → commits in main branch
D → E → commits in feature branch
Feature branch was created from C

🔥Types of :
✅ 1. Fast-Forward Merge: 👉 Happens when no divergence
👉 Divergence = both branches have new commits after branching point
Before Merge:
A ← B ← C        (main)
             \
              D ← E (feature)
👉 Here:
🔹 main branch → Created at the very beginning (from commit A)
🔹 feature branch → Created at commit C
main stopped at C
feature continued to D, E
main has no new commits after C     

🧠 Meaning
👉 Only one branch moved forward
👉 History is linear
👉 So Git can simply move main forward:
After Merge:
A ← B ← C ← D ← E   (main, feature)
👉 ✅ This is Fast-Forward (no divergence)  


✅ 2. 3-Way Merge (Normal Merge):  👉 Happens when branches diverged
A ← B ← C ← F       (main)
             \
              D ← E (feature)
🧠 What happened?
Both branches changed after C
main added F
feature added **D, E`
👉 Now history is split into two paths
⚠️ This is Divergence
👉 Two branches diverged from same base (C)
🔥 After Merge (3-Way Merge)
A ← B ← C ← F ← M
         \     /
          D ← E
👉 M = merge commit



What happens internally:
Git compares current branch & target branch
If both are same → “Already up to date”
If different:
        Git tries to combine changes
        Creates a merge commit
        If conflicts occur → you fix manually.

🎯 Key Difference       
| Case                  | Divergence? | Merge Type   |
| --------------------- | ----------- | ------------ |
| Only one branch moved | ❌ No        | Fast-Forward |
| Both branches changed | ✅ Yes       | 3-Way Merge  |



✅🔥🌳 Initial State
A ← B ← C        (main)
         \
          D ← E  (feature)

👉 Meaning:
Up to C, both branches are same
After that:
main stays at C
feature adds D, E
🔥 Now imagine this REAL situation
Someone updates main:
A ← B ← C ← F    (main)
         \
          D ← E  (feature)

👉 Now:
main has F
feature has D, E
👉 This is called: 🚨 DIVERGENCE (both branches moved forward)

===================================================================================================================

✅🔥 Divergenve Problem Solution
🚀 OPTION 1 — git merge
Command:
git checkout main
git merge feature
What Git does:
👉 Git joins both histories together
Result:
A ← B ← C ← F ← M   (main)
         \       /
          D ← E  (feature)

👉 M = merge commit

🧠 What is happening?
Git keeps:
F from main
D, E from feature
Then creates a new commit M combining both
💡 Important Point
👉 Nothing is deleted
👉 Nothing is rewritten
👉 History stays exactly as it happened



🚀 OPTION 2 — git rebase
Command:
git checkout feature
git rebase main
What Git does:
👉 Git says:
“Let me move your feature work on top of latest main”

Step-by-step:
Step 1: Remove D, E temporarily
A ← B ← C ← F   (main)
Step 2: Replay D, E on top of F
A ← B ← C ← F ← D' ← E'   (feature)
👉 D', E' = new commits (rewritten)

🧠 What changed?
Old commits (D, E) are replaced
New commits (D', E') created
History becomes straight line




🔥 Final Comparison (MOST IMPORTANT)
🔹 Merge
        D ← E
       /     \
A ← B ← C ← F ← M
👉 Branching structure remains

🔹 Rebase
A ← B ← C ← F ← D' ← E'
👉 Clean straight line
====================================================================================================================

✅⭐ 11. "Already up to date" meaning

This happens when:
Both branches point to the same commit
No new changes exist to merge

👉 That’s why your main and new were showing up to date — they had identical history.

===================================================================================================================

✅⭐ 12. Delete a branch
git branch -d new_branch
This deletes the branch pointer named new_branch.

What happens:
Git removes only the pointer named new
It does NOT delete commits

🧲 When Git allows deletion (safe delete)
-d works only when:
✔ The new branch has already been merged into the current branch
❌ If not merged → Git gives warning:
error: The branch 'new' is not fully merged.

===================================================================================================================

✅⭐ 13. git diff
Command:
git diff "Array .java"

What happens internally:
Git compares:
      Working directory file
      Last committed version
Shows line-by-line differences
Green color = something added
Red color = removed
Filename with space → must use quotes.

===================================================================================================================

✅ 14. Reset (Dangerous but useful)
🔥 git reset --hard HEAD

Discards all uncommitted changes and Makes working directory identical to latest commit

🔥 git reset --hard HEAD^
Moves branch pointer to previous commit.

HEAD^ = parent commit
HEAD^^ = grandparent commit

====================================================================================================================

✅⭐ 15. Restore

✅ 1. git restore file_name
Restores only that specific file to the state of the last committed version.

Meaning:
Undo all changes in that one file
Bring it back to how it was in the last commit
Does NOT touch other files

✅ 2. git restore .

Restores ALL changed files in the current folder to the last committed state.
Meaning:
Undo changes in every modified file
Discards all uncommitted changes
Works like “restore everything”



| Command            | Restores            | Scope                    |
| ------------------ | ------------------- | ------------------------ |
| `git restore file` | Only that file      | Specific file            |
| `git restore .`    | Every modified file | Entire working directory |

===================================================================================================================

✅⭐ 17. Remote:
git remote -v
This command shows the remote repository URLs linked to your local project.
origin  https://github.com/... (fetch)
origin  https://github.com/... (push)


origin = nickname for your GitHub URL.

====================================================================================================================




