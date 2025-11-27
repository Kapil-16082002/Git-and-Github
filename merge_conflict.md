✅⭐Git Collision (Merge Conflict):
When Git automatically merges branches, it usually works fine.
But if the same part of a file was changed in two branches, Git cannot decide which version to keep.
// (or one changed/renamed/deleted a file while the other changed it).

🟩 If only one branch changes a part of the file and the other branch keeps it same → NO conflict.
🧠 Why conflicts happen (common situations)
1. Same lines edited in the same file on two different branches
2. One branch deleted a file while the other modified it.
3. Rename + modify: file renamed on one branch, edited on other.
4. Binary files (images, .docx) — Git can’t merge; choose one version.


➡️ Conflict occurs
Branch main (file.txt):
int x = 10;

Branch dev:
int x = 20;

When you try: git merge dev
Git sees both branches changed the same line, so it cannot auto-merge.

❌ No conflict if…
They edit different lines of the same file:
main edits line 5
dev edits line 20
Then Git auto-merges without conflict.


🗂️ Tools for Easier Conflict Resolution
VSCode built-in merge tool
GitKraken
Sourcetree
IntelliJ / CLion merge tools

✅🛠️ STEP-BY-STEP: HOW TO RESOLVE MERGE CONFLICTS:

Quick checklist (before anything)
# see conflict state 
git status

# list conflicted files
git diff --name-only --diff-filter=U

# inspect conflict details in a file
git diff <file>

//==================================================================================================================

✅Method A — Manual edit (the basic way)

🧩 WHAT you see inside the conflicted file
When a conflict appears, Git inserts special conflict markers in the file:

<<<<<<< HEAD
→ This shows the version from your current branch (the branch you are on).

=======
→ This separates both versions.

>>>>>>> feature-branch
→ This shows changes from the branch you are merging into current.


🛠️ FULL STEP-BY-STEP METHOD (Manual Edit)

⭐STEP 1 — Open the conflicted file
You can use any editor:
Windows CMD:
notepad file.txt

VS Code:
code file.txt


⭐STEP 2 — Find the conflict markers
Inside the file, search for:

<<<<<<<

=======

>>>>>>>
These mark the exact area where Git is confused.


⭐STEP 3 — Decide the final content
You will see something like this:
<<<<<<< HEAD
cout << "Hello from MAIN branch";
=======
cout << "Hello from FEATURE branch";
>>>>>>> feature-branch


Now YOU must decide what the final version should be.

Possible options:
✔ Option 1 — Keep HEAD version
cout << "Hello from MAIN branch";

✔ Option 2 — Keep incoming version
cout << "Hello from FEATURE branch";

✔ Option 3 — Combine both
cout << "Hello from MAIN branch";
cout << "Hello from FEATURE branch";

✔ Option 4 — Create an entirely new custom line
cout << "Combined update by Kapil Papa jii";

⚠️ IMPORTANT:
After choosing the final content, remove the conflict markers:

<<<<<<< HEAD

=======

>>>>>>> feature-branch


⭐STEP 4 — Save the file: Ctrl + S
⭐STEP 5 — Stage the resolved file
This tells Git: I have fixed the conflict.
git add file.txt

⭐STEP 6 — Finish the merge
If you were in a merge, run:
git commit

If you were doing a rebase, run:
git rebase --continue
Git will continue applying the remaining commits.


⭐ Quick Summary for Revision — Manual Conflict Fix
1. Open file  
2. Find: <<<<<<<, =======, >>>>>>>  
3. Edit the final content  
4. Remove all markers  
5. Save  
6. git add file  
7. git commit   (for merge)
   OR
   git rebase --continue (for rebase)

//================================================================================================================

✅⭐Method B — Accept one side entirely and Discard other (pick ours / theirs):
keep one version and discard the other. 
Use this when you want to keep either the current branch (ours/HEAD) or the other branch (theirs).

Use this method when:
You don’t want to manually edit the conflicted file
You want to fully keep one version and discard the other
You want a quick resolution without combining changes

🧩 First understand: What is OURS and THEIRS?
⭐ OURS
Means: current branch (the branch you are currently on). Git calls it HEAD

⭐ THEIRS
Means: the branch you are merging into current
Example: if you are on main and you run:
        git merge feature
        OURS = main
        THEIRS = feature
📌 Example of conflict
Suppose file has conflict markers:
<<<<<<< HEAD
cout << "Main branch version";
=======
cout << "Feature branch version";
>>>>>>> feature

If you pick OURS → keep MAIN version
If you pick THEIRS → keep FEATURE version

🛠️ Option 1: Keep CURRENT branch version (OURS)
If you want to completely ignore incoming changes and keep your current branch version, use:
git checkout --ours -- path/to/file.txt
git add path/to/file.txt
git commit


🧠 Meaning:
git checkout --ours → Replace conflicted file with your version
git add → Mark as resolved
git commit → Finish merge
When to use:
✅ You trust your branch
✅ Incoming branch has wrong/broken/unwanted changes
✅ You want to override their version completely


🛠️ Option 2: Keep INCOMING branch version (THEIRS)
If you want to discard your version and keep the version from merged branch, use:
git checkout --theirs -- path/to/file.txt
git add path/to/file.txt
git commit

🧠 Meaning:
git checkout --theirs → Replace conflicted file with the incoming branch version
git add → Mark resolved
git commit → Finish merge
When to use:
✅ Their version is correct
✅ You want your file to match that branch
✅ You don't need your changes


//=================================================================================================================

✅⭐ Method C — Resolve Merge Conflicts Using git mergetool (GUI Tools)
This method is perfect if you prefer a visual tool instead of manually editing text.

🔥 What is a mergetool?
A mergetool is a graphical interface (GUI) that shows:
OURS version
THEIRS version
BASE version (original file before both branches edited it)
And lets you choose or combine content visually.
No need to manually type or find conflict markers.

🎯 Why use Mergetool?
Because it:
✔ Provides buttons to pick “ours” or “theirs”
✔ Makes conflicts easier to SEE
✔ Colors changes
✔ Avoids mistakes
✔ Faster for big files

🧠 Examples of mergetools:
VS Code (most common)
KDiff3
Meld
Beyond Compare
P4Merge
WinMerge

🚀 STEP 1 — Configure a mergetool
⭐ Example: Configure VS Code as mergetool
Run these commands once (only first time):
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd "code --wait $MERGED"

What this does:
Tells Git that your merge tool is VS Code
When Git calls for merge, it runs:
"code --wait"
meaning: open file in VS Code and wait until you close it


🚀 STEP 2 — Run mergetool
When a merge conflict occurs, simply run:
What happens next:
A GUI opens (VS Code window)
Each conflicted file opens one by one
You see:
✔ OURS version
✔ THEIRS version
✔ Base version
✔ Final merged output panel


In VS Code:
You get clickable options:
Accept Current Change (OURS)
Accept Incoming Change (THEIRS)
Accept Both Changes
Compare changes
Manual editing in the final window

📝 After resolving in GUI:
Simply Save and Close.
Git will automatically treat the file as resolved.
You do not need git add after using mergetool — Git does it.

🚀 STEP 3 — Finish merge
After all files are resolved:  git commit
This completes the merge.


⭐ Alternative Method (VS Code only)

VS Code itself shows a built-in merge conflict interface.
Just open your project:
code .

VS Code will show:
Side-by-side conflicts
Highlighted blocks
Buttons to accept/reject changes
Fix all files manually, then:
git add -A
git commit


🏁 FINAL SUMMARY (Very Easy to Remember)
| Step | Action                                  |
| ---- | --------------------------------------- |
| 1    | Configure mergetool (VS Code or others) |
| 2    | Run `git mergetool`                     |
| 3    | Resolve conflicts visually              |
| 4    | Save & close GUI                        |
| 5    | Git auto-stages the file                |
| 6    | Run `git commit` to finish              |

