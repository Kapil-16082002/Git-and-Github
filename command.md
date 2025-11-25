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

//=================================================================================================================

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
| ---------------- | --------------------------------------- |
| Branch           | A pointer to a commit                   |
| Commit           | A node linked to the previous commit    |
| HEAD             | Points to the current branch            |
| `git branch x`   | Creates a pointer at the current commit |
| `git checkout x` | Moves HEAD to that branch               |
| New commit       | Moves only the current branch pointer   |



//==================================================================================================================

✅⭐ 1. What is git init?
Command: git init

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

//================================================================================================================

✅⭐ 2. What is git clone?
Command:
git clone <repo-url>

What happens internally:
Git downloads the entire remote repo (all branches + commits)
Creates a new folder with the project contents
Automatically sets origin as the remote (GitHub link)
This is used when working on existing GitHub projects.

//===============================================================================================================

✅⭐ 3. What is git status?

Shows:
git status shows what is where.
files you changed
files not tracked
files staged for commit

Git divides files into 3 areas:

| Area                     | Meaning               |
| ---------------------    | --------------------- |
| 1. **Working directory** | Your actual files     |
| 2. **Staging area**      | Files ready to commit |
| 3. **Repository**        | Saved commits         |

//=============================================================================================================

✅⭐ 4. What is git add?
Command:  git add file.java

git add file.java moves file.java from:
👉 Working Directory → Staging Area
This means the file is now prepared for the next commit.
Staging area = "final preparation room" before commit.

//=================================================================================================================

✅⭐ 5. What is git commit?
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

//=================================================================================================================

✅⭐ 6. What is git log?
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


//=================================================================================================================

✅⭐ 7. What is a Branch?
Think of Branch like:
A separate copy of code, made for working safely without touching main.

What happens internally:
Branch is just a pointer to a commit
main points to last commit
new-feature can point to another commit

No heavy copy is made.
Git branches are very light and fast.
| Command                         | Meaning                            |                 
| ------------------------------- | ---------------------------------- |
| `git branch`                    | Shows **all branches** in the repo |
| 'git branch | grep branch_Name  |Show only a specific branch_name    |
|  git branch -v branchName       | Display detailed info about a single branch |
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

//=================================================================================================================

✅⭐ 9. git checkout <branch>

Switch branch:

git checkout new_branch

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
| `git checkout <commitHash>`              | Checkout a **specific commit** → Detached HEAD mode              |
| `git checkout branchName -- fileName`    | Bring **only that file** from another branch into current branch |
| `git checkout -- fileName`               | Discard changes → Restore file to last committed version         |
| `git checkout -t origin/branchName`      | Checkout a **remote branch** and start tracking it               |
| `git checkout -b newBranch <commitHash>` | Create a new branch starting from an **older commit**            |

//=================================================================================================================

✅⭐ 10. git merge
Command: git merge new

What happens internally:
Git compares current branch & target branch
If both are same → “Already up to date”
If different:
        Git tries to combine changes
        Creates a merge commit
        If conflicts occur → you fix manually.

//=================================================================================================================

✅⭐ 11. "Already up to date" meaning

This happens when:
Both branches point to the same commit
No new changes exist to merge

👉 That’s why your main and new were showing up to date — they had identical history.

//=================================================================================================================

✅⭐ 12. Delete a brancgit branch -d new_branch
This deletes the branch pointer named new_branch.

What happens:
Git removes only the pointer named new
It does NOT delete commits

🧲 When Git allows deletion (safe delete)
-d works only when:
✔ The new branch has already been merged into the current branch
❌ If not merged → Git gives warning:
error: The branch 'new' is not fully merged.



//=================================================================================================================

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

//=================================================================================================================

✅ 14. Reset (Dangerous but useful)
🔥 git reset --hard HEAD

Discards all uncommitted changes
Makes working directory identical to latest commit

🔥 git reset --hard HEAD^
Moves branch pointer to previous commit.

HEAD^ = parent commit
HEAD^^ = grandparent commit

//=================================================================================================================

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


//=================================================================================================================

✅⭐ 16. Push & Pull
git push : Uploads commits to GitHub.
git pull: Downloads latest commits from GitHub.

Internally:
Git fetches new commits
Merges them into your branch

//=================================================================================================================

✅⭐ 17. Remote:
git remote -v
This command shows the remote repository URLs linked to your local project.
origin  https://github.com/... (fetch)
origin  https://github.com/... (push)


origin = nickname for your GitHub URL.

//=================================================================================================================
