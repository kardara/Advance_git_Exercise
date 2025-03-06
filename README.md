```markdown
# Part 1: Refining Git History (10 Challenges)

## Challenge 1: Missing File Fix

1. **Check the current repository status**  
   Run the following command to see the current state of the repository:

   ```bash
   git status
   ```

   Output:
   ```bash
   On branch master
   Your branch is based on 'origin/master', but the upstream is gone.
     (use "git branch --unset-upstream" to fixup)

   Untracked files:
     (use "git add <file>..." to include in what will be committed)

           README.md
           test4.md

   nothing added to commit but untracked files present (use "git add" to track)
   ```

2. **Stage the missing file**  
   To stage the missing file (`test4.md`), use the following command:

   ```bash
   git add test4.md
   ```

3. **Amend the last commit**  
   Now, amend the previous commit to include the missing file:

   ```bash
   git commit --amend -m "Add missing test4.md file"
   ```

   Output:
   ```bash
   [master 4fd309f] Add missing test4.md file
    Date: Wed Feb 26 11:12:37 2025 +0200
    2 files changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 test3.md
    create mode 100644 test4.md
   ```

## Challenge 2: Editing Commit History
1. **Check the logs to see all the commit**
   ```bash
   git log
   ```
   Output: 
```bash
   commit 63f5020ebd458eefe0a1fb30caad9b03394874cd (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:25:30 2025 +0200

    creating another file

commit 694932e0f805cef912d559db9f7999fd8137a9f2
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:15:40 2025 +0200

    adding readme file

commit 266646e1de09f8b814abc9e5ffe5873e550b49ea
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:06:18 2025 +0200

    Create another file

commit ef0cac950e61caef08dfa237bd8bc6fb53fc2b9e (origin/master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 11:34:39 2025 +0200
```
   
2. **let change The commit message "Create another file" needs to be changed to "adiing readme.md".**
   ```bash
   git rebase -i HEAD~2
   ```
   outPut:
```bash
pick 694932e adding readme file
pick 63f5020 creating another file

# Rebase 266646e..63f5020 onto 266646e (2 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```
As I'm usng vim editor, we change the commit from pick to reword, and we do `shift + ':'wq`

output:
```bash
creating another file

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Wed Feb 26 12:25:30 2025 +0200
#
# interactive rebase in progress; onto 266646e
# Last commands done (2 commands done):
#    pick 694932e adding readme file
#    reword 63f5020 creating another file
# No commands remaining.
# You are currently editing a commit while rebasing branch 'master' on '266646e'.
#
# Changes to be committed:
#       modified:   README.md
#
~
"~/kardara/advance_git/Advance_git_Exercise/.git/COMMIT_EDITMSG" 17L, 534B
```
we change the text, and we save and quite

Output:
```bash
ymubutwari@Ubutwaris-iMac Advance_git_Exercise % git rebase -i HEAD~2                 
[detached HEAD 1a38fe3] adding readme.md
 Date: Wed Feb 26 12:25:30 2025 +0200
 1 file changed, 5 insertions(+), 1 deletion(-)
Successfully rebased and updated refs/heads/master.
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
And after redoing `git log`, we get:

```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log             
commit 1a38fe332b33ba377635d90da7bb43038030c91c (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:25:30 2025 +0200

    adding readme.md

commit 694932e0f805cef912d559db9f7999fd8137a9f2
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:15:40 2025 +0200

    adding readme file

commit 266646e1de09f8b814abc9e5ffe5873e550b49ea
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:06:18 2025 +0200

    Create another file

commit ef0cac950e61caef08dfa237bd8bc6fb53fc2b9e (origin/master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 11:34:39 2025 +0200
```
## Challenge 3. Keeping History Tidy - Squashing Commits
 The commit "Create second file" should be merged into "Create initial file" for a cleaner history.

```sh
git log
```
Output:
```sh
commit 63f5020ebd458eefe0a1fb30caad9b03394874cd (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:25:30 2025 +0200

    Create another file

commit 694932e0f805cef912d559db9f7999fd8137a9f2
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:15:40 2025 +0200

    adding readme file
```

To squash commits:
1. Run:
   ```sh
   git rebase -i HEAD~2
   ```
2. Change `pick` to `squash`:
   ```sh
   pick 694932e adding readme file
   squash 63f5020 creating another file
   ```
3. Edit the commit message and save.

Final log:
```sh
git log
```
Output:
```sh
commit 1a38fe332b33ba377635d90da7bb43038030c91c (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:25:30 2025 +0200

    adding readme.md

commit 694932e0f805cef912d559db9f7999fd8137a9f2
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:15:40 2025 +0200

    adding readme file
```

## Challenge 4. Splitting a Commit
Imagine "Create test5 and test6 files" describes too much at once. so let's Separate them for better tracking with two different commit messages: "Create test5 File" and "Create test6 file".
### 1. Let's check the log before spliiting
```bash
git log
```
Output:
```bash
uthor: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 11:42:38 2025 +0200

    Create test5 and test6

commit 60c2b1c0cd1721f7a402507bc5e66458054a446a (origin/master, origin/HEAD)
Merge: 35bd99b abce601
Author: kardara <abdoulayekardara@gmail.com>
Date:   Wed Feb 26 12:41:33 2025 +0200
```
### 2. Reset the commit while keeping the changes
```bash
git reset HEAD~1
```
OutPut: 
```bash
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git reset HEAD~1
Unstaged changes after reset:
M       README.md
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise>
```
### 3. Add and commit the third file separately
```bash
git add test5.md
git commit -m "Create test5 File"
```
### 4. Add and commit the fourth file separately
```bash
git add test6.md
git commit -m "Create test6 File"
```
### Now let's do git log and see after splitting
```bash
git log
```
OutPut: 
```bash
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 11:51:21 2025 +0200

    Create test6 File

commit 231c36a17cbd5c0c2c861d3ba066a002872fb067
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 11:50:02 2025 +0200

    Create test5 File
```
## Challenge 5. Advanced Squashing
Let's combine the 2 last commits("Create test5 File" and "Create test6 File"). We can use the same steps as we did in challenge 3

### 1. Let's check logs
```bash
git log
```
OutPut: 
```bash
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 11:51:21 2025 +0200

    Create test6 File

commit 231c36a17cbd5c0c2c861d3ba066a002872fb067
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 11:50:02 2025 +0200

    Create test5 File
```
### 2. Start an interactive rebase
```bash
git rebase -i HEAD~2
```
### 3. Change pick to squash for the second commit.

### 4.Modify the commit message to "Create test5 and test6 files" and save.

outPut: 
```bash
commit 1fda2798706b5c08d1bc3f24ae1a625aa7d28a8f (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 11:50:02 2025 +0200

    Create test5 and test6
    
    Create test5 File
    
    Create test6 File

commit 60c2b1c0cd1721f7a402507bc5e66458054a446a (origin/master, origin/HEAD)
Merge: 35bd99b abce601
:
```
### Challenge 6. Dropping a Commit:

We all make mistakes. Imagine needing to completely remove an unwanted commit from your history.

Let's Create a new file named unwanted.txt add some changes and commit it with a message like "Unwanted commit".

Challenge: Use git rebase -i to identify and remove the "Unwanted commit" commit, cleaning up your history. learn more about dropping commits
```bash
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> New-Item unwanted.txt -ItemType File


    Directory: C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          3/3/2025   1:29 PM              0 unwanted.txt


PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git add unwanted.txt  
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git commit -m "Unwanted commit"
[master cc16358] Unwanted commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 unwanted.txt
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git log
commit cc163587e7cd21df3b929bbb98fb32e4776f716b (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 13:29:39 2025 +0200

    Unwanted commit

commit 169c887c63c36f5bad057ac5088b9d9266cd06a3 (origin/master, origin/HEAD)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 13:08:12 2025 +0200

    last commit

PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git rebase -i HEAD~2
Successfully rebased and updated refs/heads/master.
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> 
```
## Challenge 6. Dropping a Commit:

We all make mistakes. Imagine needing to completely remove an unwanted commit from your history.

Let's Create a new file named unwanted.txt add some changes and commit it with a message like "Unwanted commit".

Challenge: Use git rebase -i to identify and remove the "Unwanted commit" commit, cleaning up your history. learn more about dropping commits
```bash
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> New-Item unwanted.txt -ItemType File


    Directory: C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          3/3/2025   1:29 PM              0 unwanted.txt


PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git add unwanted.txt  
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git commit -m "Unwanted commit"
[master cc16358] Unwanted commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 unwanted.txt
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git log
commit cc163587e7cd21df3b929bbb98fb32e4776f716b (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 13:29:39 2025 +0200

    Unwanted commit

commit 169c887c63c36f5bad057ac5088b9d9266cd06a3 (origin/master, origin/HEAD)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 13:08:12 2025 +0200

    last commit

PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git rebase -i HEAD~2
Successfully rebased and updated refs/heads/master.
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> 
```
## Challenge 7. Reordering Commits

Challenge: Use `git rebase -i` to change the order of commits in your history.
1. Run: `git rebase -i HEAD~3`

2. Change the order of the commits in the interactive editor by rearranging the lines.

3. Save and close the editor.
```bash
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git log
commit 8031df57acd349dc98d79b81472043db8c4e4e15 (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 13:45:11 2025 +0200

    Chore: adding readme file after challenge 6

commit fcb5fdfa7c53ecd7f6550b2fc24cc23e92249a21
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 14:15:52 2025 +0200

    this is a commit before reordering

PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git rebase -i HEAD~2
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git log              
commit 861d36da61ed8d823cffb665b0415d594b81cd60 (HEAD -> master)
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 14:15:52 2025 +0200

    this is a commit before reordering

commit ef6bfedfa600f94569cdf72eb830726215f0d9d2
Author: kardara <abdoulayekardara@gmail.com>
Date:   Mon Mar 3 13:45:11 2025 +0200

    Chore: adding readme file after challenge 6

:
```
## Challenge 8. Cherry-Picking Commits

**Challenge: Selectively bring a specific commit from another branch into your current branch.**

1. **Create a new branch and add a new file:**
   ```sh
   git checkout -b ft/branch
   touch test5.md
   echo "Test 5 content" > test5.md
   git add test5.md
   git commit -m "Implemented test 5"
   ```
2. **Switch back to the main branch:**
   ```sh
   git checkout main
   ```
3. **Find the commit hash of the commit you want to cherry-pick:**
   ```sh
   git log ft/branch --oneline
   ```
4. **Copy the cammit-hash and do:**
   ```sh
   git cherry-pick <commit-hash>
   ```
Output: 
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git checkout master        
Already on 'master'
Your branch is up to date with 'origin/master'.
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log ft/branch --oneline
9f3cdfd (ft/branch) Implemented test 5
d1d92fa (HEAD -> master, origin/master) Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
e6d0e49 Chore: committing after challenge 7
861d36d this is a commit before reordering
ef6bfed Chore: adding readme file after challenge 6
b9a8165 Chore: adding readme file after challenge 6
169c887 last commit
1fda279 Create test5 and test6
60c2b1c Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
35bd99b chore: last commit
1a38fe3 adding readme.md
694932e adding readme file
266646e Create another file
abce601 Update README.md
ef0cac9 adding readme
4fd309f Add missing test4.md file
4075fbc chore: Create another file
055454a chore: Create initial file
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git cherry-pick 9f3cdfd      
[master 3ddeeb3] Implemented test 5
 Date: Tue Mar 4 13:32:40 2025 +0200
 1 file changed, 1 insertion(+)
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log --oneline
3ddeeb3 (HEAD -> master) Implemented test 5
d1d92fa (origin/master) Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
e6d0e49 Chore: committing after challenge 7
861d36d this is a commit before reordering
ef6bfed Chore: adding readme file after challenge 6
b9a8165 Chore: adding readme file after challenge 6
169c887 last commit
1fda279 Create test5 and test6
60c2b1c Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
35bd99b chore: last commit
1a38fe3 adding readme.md
694932e adding readme file
266646e Create another file
abce601 Update README.md
ef0cac9 adding readme
4fd309f Add missing test4.md file
4075fbc chore: Create another file
055454a chore: Create initial file
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
## Cahllenge 9. Visualizing Commit History (Bonus)
**Challenge**: Explore ways to visualize commit history.

Use a graphical tool or command: `git log --graph` 

or `git log --graph --oneline --all`

OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log --graph
* commit e9052f2f31eac3aa5073f8a3e43e7d9c4d98ee3c (HEAD -> master, origin/master)
| Author: kardara <abdoulayekardara@gmail.com>
| Date:   Tue Mar 4 13:53:56 2025 +0200
| 
|     adding readme after challenge 8
| 
* commit 3ddeeb31acbb27aa3f2c454a5b9d192727e345f2
| Author: kardara <abdoulayekardara@gmail.com>
| Date:   Tue Mar 4 13:32:40 2025 +0200
| 
|     Implemented test 5
|   
*   commit d1d92fa07e4e9364816e2e06894df28cf8695fbe
|\  Merge: e6d0e49 b9a8165
| | Author: kardara <abdoulayekardara@gmail.com>
| | Date:   Mon Mar 3 14:34:52 2025 +0200
| | 
| |     Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
| | 
| * commit b9a81650fbb25d3232a84730ac339d5a369e3782
| | Author: kardara <abdoulayekardara@gmail.com>
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log --graph --oneline --all
* e9052f2 (HEAD -> master, origin/master) adding readme after challenge 8
* 3ddeeb3 Implemented test 5
| * 9f3cdfd (ft/branch) Implemented test 5
|/  
*   d1d92fa Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
|\  
| * b9a8165 Chore: adding readme file after challenge 6
* | e6d0e49 Chore: committing after challenge 7
* | 861d36d this is a commit before reordering
* | ef6bfed Chore: adding readme file after challenge 6
|/  
* 169c887 last commit
* 1fda279 Create test5 and test6
*   60c2b1c Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
|\  
| * abce601 Update README.md
* | 35bd99b chore: last commit
* | 1a38fe3 adding readme.md
* | 694932e adding readme file
* | 266646e Create another file
|/  
:
```
## Cahllenge 10. Understanding Reflogs
**Challenge:** Learn about `git reflog` to track Git operations history.

**Solution:**

- View the reflog:
  ```sh
  git reflog
  ```
- Use it to revert to a previous state if needed:
  ```sh
  git reset --hard <commit-hash>
  ```
Output: 
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git reflog
0b40aab (HEAD -> master, origin/master) HEAD@{0}: commit: adding readme after challenge 9
51dfee7 HEAD@{1}: commit: adding readme after challenge 9
e9052f2 HEAD@{2}: commit: adding readme after challenge 8
3ddeeb3 HEAD@{3}: cherry-pick: Implemented test 5
d1d92fa HEAD@{4}: checkout: moving from master to master
d1d92fa HEAD@{5}: checkout: moving from ft/branch to master
9f3cdfd (ft/branch) HEAD@{6}: commit: Implemented test 5
d1d92fa HEAD@{7}: checkout: moving from master to ft/branch
d1d92fa HEAD@{8}: pull: Fast-forward
60c2b1c HEAD@{9}: pull: Merge made by the 'recursive' strategy.
35bd99b HEAD@{10}: commit: chore: last commit
1a38fe3 HEAD@{11}: rebase -i (finish): returning to refs/heads/master
1a38fe3 HEAD@{12}: rebase -i (reword): adding readme.md
63f5020 HEAD@{13}: rebase -i: fast-forward
694932e HEAD@{14}: rebase -i (start): checkout HEAD~2
63f5020 HEAD@{15}: commit: creating another file
694932e HEAD@{16}: rebase -i (finish): returning to refs/heads/master
694932e HEAD@{17}: rebase -i (reword): adding readme file
605def7 HEAD@{18}: rebase -i: fast-forward
266646e HEAD@{19}: rebase -i (start): checkout HEAD~2
605def7 HEAD@{20}: commit: adding something
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git reset --hard 9f3cdfd      
HEAD is now at 9f3cdfd Implemented test 5
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git reflog              
9f3cdfd (HEAD -> master, ft/branch) HEAD@{0}: reset: moving to 9f3cdfd
0b40aab (origin/master) HEAD@{1}: commit: adding readme after challenge 9
51dfee7 HEAD@{2}: commit: adding readme after challenge 9
e9052f2 HEAD@{3}: commit: adding readme after challenge 8
3ddeeb3 HEAD@{4}: cherry-pick: Implemented test 5
d1d92fa HEAD@{5}: checkout: moving from master to master
d1d92fa HEAD@{6}: checkout: moving from ft/branch to master
9f3cdfd (HEAD -> master, ft/branch) HEAD@{7}: commit: Implemented test 5
d1d92fa HEAD@{8}: checkout: moving from master to ft/branch
d1d92fa HEAD@{9}: pull: Fast-forward
60c2b1c HEAD@{10}: pull: Merge made by the 'recursive' strategy.
35bd99b HEAD@{11}: commit: chore: last commit
1a38fe3 HEAD@{12}: rebase -i (finish): returning to refs/heads/master
1a38fe3 HEAD@{13}: rebase -i (reword): adding readme.md
63f5020 HEAD@{14}: rebase -i: fast-forward
694932e HEAD@{15}: rebase -i (start): checkout HEAD~2
63f5020 HEAD@{16}: commit: creating another file
694932e HEAD@{17}: rebase -i (finish): returning to refs/heads/master
694932e HEAD@{18}: rebase -i (reword): adding readme file
605def7 HEAD@{19}: rebase -i: fast-forward
266646e HEAD@{20}: rebase -i (start): checkout HEAD~2
```
# Part 2: Branching Basics 
## Challenge 1. Feature Branch Creation

Solution:
**Challenge:** Create a new branch named ft/new-feature and switch to that branch.
```bash
git checkout -b ft/new-feature
```
>This command creates a new branch and switches to it immediately, allowing isolated development.

OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git checkout -b ft/new-feature
M       README.md
Switched to a new branch 'ft/new-feature'
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
## Challenge 2. Working on the Feature Branch
**Challenge:** Create a new file named `feature.txt` in this branch, add content, and commit it.

Solution:
```bash
echo "This is the core functionality for the new feature." > feature.txt
git add feature.txt
git commit -m "Implemented core functionality for new feature"
```
> This ensures changes are tracked and saved with a meaningful commit message.

OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % echo "This is the core functionality for the new feature." > feature.txt
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git add feature.txt
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git commit -m "Implemented core functionality for new feature"
[ft/new-feature 234fc2d] Implemented core functionality for new feature
 1 file changed, 1 insertion(+)
 create mode 100644 feature.txt
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
## Challenge 3. Switching Back and Making More Changes
**Challenge:** Switch back to `master` and create a `readme.txt` file.

Solution:
```bash
git checkout master
echo "Project README" > readme.txt
git add readme.txt
git commit -m "Updated project readme"
```
OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git checkout master

M       README.md
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % echo "Project README" > readme.txt

gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git add readme.txt
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git commit -m "Updated project readme"
[master 95e308c] Updated project readme
 1 file changed, 1 insertion(+)
 create mode 100644 readme.txt
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
## Challenge 4. Local vs. Remote Branches
**Challenge:** Research remote branches and push your local branch to a remote repository.

Solution:
```bash
git push origin ft/new-feature
```
> This command pushes the local branch to the remote repository, making it accessible to others for collaboration and ensuring that work is backed up on a remote server.

OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git push origin ft/new-feature

Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 341 bytes | 341.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'ft/new-feature' on GitHub by visiting:
remote:      https://github.com/kardara/Advance_git_Exercise/pull/new/ft/new-feature
remote: 
To https://github.com/kardara/Advance_git_Exercise.git
 * [new branch]      ft/new-feature -> ft/new-feature
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
## Challenge 5. Branch Deletion
**Challenge:** Delete the `ft/new-feature` branch after merging it into `main`.

Solution:
```bash
git branch -d ft/new-feature
```

> Using `-d` ensures the branch is deleted only if it has been fully merged. If you need to force deletion, use `-D` instead.

OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git branch -d ft/new-feature

error: The branch 'ft/new-feature' is not fully merged.
If you are sure you want to delete it, run 'git branch -D ft/new-feature'.
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git branch -D ft/new-feature

Deleted branch ft/new-feature (was 234fc2d).
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```

## Challenge 6. Creating a Branch from a Commit
**Challenge:** Create a branch from a commit two positions back.
```bash
git log --oneline  # Displays commit history in a condensed form to find the commit hash.
git checkout -b ft/new-branch-from-commit <commit-hash> #Creates a new branch starting from a specific commit, useful for revisiting an earlier state of the project.
```

OutPut: 
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log --oneline 
95e308c (HEAD -> master) Updated project readme
7315728 (origin/master) adding readme after challenge 10
14a12e7 Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
0b40aab adding readme after challenge 9
51dfee7 adding readme after challenge 9
e9052f2 adding readme after challenge 8
3ddeeb3 Implemented test 5
9f3cdfd (ft/branch) Implemented test 5
d1d92fa Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
e6d0e49 Chore: committing after challenge 7
861d36d this is a commit before reordering
ef6bfed Chore: adding readme file after challenge 6
b9a8165 Chore: adding readme file after challenge 6
169c887 last commit
1fda279 Create test5 and test6
60c2b1c Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
35bd99b chore: last commit
1a38fe3 adding readme.md
694932e adding readme file
266646e Create another file
abce601 Update README.md
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git checkout -b ft/new-branch-from-commit 95e308c
M       README.md
Switched to a new branch 'ft/new-branch-from-commit'
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```

## Challenge 7. Branch Merging
**Challenge:** Merge ft/new-branch-from-commit into main.

Solution:
```bash 
git checkout master #Switches to the master branch to prepare for merging.
git merge ft/new-branch-from-commit #Merges changes from ft/new-branch-from-commit into master, integrating updates.
```
OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git checkout master
M       README.md
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git merge ft/new-branch-from-commit
Already up to date.
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
## Challenge 8. Branch Rebasing
**Challenge:** Rebase ft/new-branch-from-commit onto main.

Solution:
```bash
git checkout ft/new-branch-from-commit #Switches to the branch to be rebased.
git rebase master #Re-applies changes from ft/new-branch-from-commit on top of master, keeping the commit history linear.
```

OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git checkout ft/new-branch-from-commit
Switched to branch 'ft/new-branch-from-commit'
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git rebase master                     
First, rewinding head to replay your work on top of it...
Fast-forwarded ft/new-branch-from-commit to master.
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
## Challenge 9. Renaming Branches
**Challenge:** Rename ft/new-branch-from-commit to ft/improved-branch-name.

Solution:
```bash
git branch -m ft/new-branch-from-commit ft/improved-branch-name
```

OutPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git branch                                                     
  ft/branch
* ft/new-branch-from-commit
  master
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git branch -m ft/new-branch-from-commit ft/improved-branch-name
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git branch                                                     
  ft/branch
* ft/improved-branch-name
  master
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
## Challenge 10. Checking Out Detached HEAD
**Challenge:** Detach HEAD to inspect a previous commit.

Solution:
```bash
git log --oneline # to check the commit history and get the commit-has
git checkout <commit-hash>
```

OUtPut:
```bash
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log --oneline
0ab17f4 (HEAD -> master, origin/master) adding the readme file after part 2 challenge 10
f8c6b4a adding the readme file after part 2 challenge 10
fdd64ea (ft/improved-branch-name) adding readme
95e308c Updated project readme
7315728 adding readme after challenge 10
14a12e7 Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
0b40aab adding readme after challenge 9
51dfee7 adding readme after challenge 9
e9052f2 adding readme after challenge 8
3ddeeb3 Implemented test 5
9f3cdfd (ft/branch) Implemented test 5
d1d92fa Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
e6d0e49 Chore: committing after challenge 7
861d36d this is a commit before reordering
ef6bfed Chore: adding readme file after challenge 6
b9a8165 Chore: adding readme file after challenge 6
169c887 last commit
1fda279 Create test5 and test6
60c2b1c Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
35bd99b chore: last commit
1a38fe3 adding readme.md
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git checkout 35bd99b
Note: checking out '35bd99b'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 35bd99b... chore: last commit
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log --oneline   
35bd99b (HEAD) chore: last commit
1a38fe3 adding readme.md
694932e adding readme file
266646e Create another file
ef0cac9 adding readme
4fd309f Add missing test4.md file
4075fbc chore: Create another file
055454a chore: Create initial file
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git checkout master 
Previous HEAD position was 35bd99b... chore: last commit
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git log --oneline  
0ab17f4 (HEAD -> master, origin/master) adding the readme file after part 2 challenge 10
f8c6b4a adding the readme file after part 2 challenge 10
fdd64ea (ft/improved-branch-name) adding readme
95e308c Updated project readme
7315728 adding readme after challenge 10
14a12e7 Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
0b40aab adding readme after challenge 9
51dfee7 adding readme after challenge 9
e9052f2 adding readme after challenge 8
3ddeeb3 Implemented test 5
9f3cdfd (ft/branch) Implemented test 5
d1d92fa Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
e6d0e49 Chore: committing after challenge 7
861d36d this is a commit before reordering
ef6bfed Chore: adding readme file after challenge 6
b9a8165 Chore: adding readme file after challenge 6
169c887 last commit
1fda279 Create test5 and test6
60c2b1c Merge branch 'master' of https://github.com/kardara/Advance_git_Exercise
35bd99b chore: last commit
1a38fe3 adding readme.md
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```

# Part 3. Advanced Workflows
### Cahllenge 1. Stashing Changes
**Scenario**:
You're working on some changes in the main branch but need to attend to something urgent. You don't want to lose your uncommitted work.

Solution:
```sh
git stash #This temporarily saves your changes, allowing you to return to them later.
```
OutPut: 
```sh
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git stash
Saved working directory and index state WIP on master: f6c442e adding the readme file after finishing  part 2 challenge 10
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise>
```
### Challenge 2. Retrieving Stashed Changes
**Scenario**:
You need to retrieve your stashed changes and continue working.

**Solution**:
```sh
git stash pop #This applies the most recent stash and removes it from the stash list.
```
OutPut: 
```sh
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git stash pop
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (cf211f529db485083b2e257ab387c5d7683cd40b)
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise>
```

### Challenge 3. Branch Merging Conflicts

**Scenario**:
You have conflicting changes in the main branch and a feature branch.

**Solution**:
##### 1. Create a new feature branch:
```sh
git checkout -b feature-branch
```
##### 2. Modify a file and commit:
```sh
echo "Feature branch change" >> file.txt
git add file.txt
git commit -m "Updated file.txt in feature-branch"
```
##### 3. Switch back to master and modify the same file:
```sh
git checkout master
echo "Main branch change" >> file.txt
git add file.txt
git commit -m "Updated file.txt in main"
```
##### 4. Merge the feature branch:
```sh
git merge feature-branch
```
##### 5. Git will report a conflict. Open the file in a text editor and manually resolve it.

##### 6.After resolving, add and commit the changes:
```sh
git add file.txt
git commit -m "Resolved merge conflict"
```

OutPut: 
```sh
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git checkout -b feature-branch
Switched to a new branch 'feature-branch'
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> echo "Feature branch change" >> file.txt
>> git add file.txt
>> git commit -m "Updated file.txt in feature-branch"
[feature-branch 2bd895c] Updated file.txt in feature-branch
 1 file changed, 0 insertions(+), 0 deletions(-)
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git checkout master
>> echo "Main branch change" >> file.txt
>> git add file.txt
>> git commit -m "Updated file.txt in main"
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
[master f62ba92] Updated file.txt in main
 1 file changed, 0 insertions(+), 0 deletions(-)
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git merge feature-branch
warning: Cannot merge binary files: file.txt (HEAD vs. feature-branch)
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
Automatic merge failed; fix conflicts and then commit the result.
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git add file.txt
>> git commit -m "Resolved merge conflict"
[master 4af13a7] Resolved merge conflict
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> 
```
### Challenge 4. Resolving Merge Conflicts with a Merge Tool

**Scenario**:
Using `git mergetool` to resolve conflicts.

**Solution**:
```sh
git mergetool #This opens the configured merge tool to help resolve conflicts visually.
```
As i do not have anything to be merge, I got `No files need merging` as output.

### Challenge 5. Understanding Detached HEAD State
**Scenario**:
Checking out a previous commit detaches the HEAD.

**Solution**:
```sh
git checkout <commit-hash>
```
To recover:
```sh
git checkout master
```
OutPut: 
```sh
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git log --oneline
c37e624 (HEAD -> master, origin/master, origin/HEAD) Chore: Pushing after part 3 challenge 4
4af13a7 Resolved merge conflict
f62ba92 Updated file.txt in main
2bd895c (feature-branch) Updated file.txt in feature-branch
b7cae05 Updated file.txt in feature-branch
18bbd3a Updated file.txt in master
2edc94a Chore: Pushing after part 3 challenge 2
f6c442e adding the readme file after finishing  part 2 challenge 10
0ab17f4 adding the readme file after part 2 challenge 10
f8c6b4a adding the readme file after part 2 challenge 10
fdd64ea adding readme
95e308c Updated project readme
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git checkout fdd64ea
Note: switching to 'fdd64ea'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at fdd64ea adding readme
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> git checkout master 
Previous HEAD position was fdd64ea adding readme
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
PS C:\Users\USER\Desktop\Git_Exercises\Advance_git_Exercise> 
```
### Challenge 6. Ignoring Files/Directories
**Scenario**:
Excluding temporary files from Git tracking.

**Solution**:
1. Create a .gitignore file and add:

```sh
/tmp
```
2. Then commit the changes:
```sh
git add .gitignore
git commit -m "Added .gitignore to exclude /tmp"
```
OutPut:
```sh
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git add .gitignore
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git commit -m "Added .gitignore to exclude /tmp"
[master 398af3e] Added .gitignore to exclude /tmp
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```
### Challenge 7.Working with Tags

**Scenario**:
Tagging a specific commit.

**Solution**:
```sh
git tag v1.0
```

### Challenge 8. Listing and Deleting Tags
**Solution**:
1. List tags:
```sh
git tag
```
2. Delete a tag:
```sh
git tag -d v1.0
```
OutPut: 
```sh
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git tag     
v1.0
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git tag -d v1.0
Deleted tag 'v1.0' (was 398af3e)
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```

### Challenge 9. Pushing Local Work to Remote
**Scenario**:
Pushing changes to a remote repository.

**Solution**:
```sh
git push origin master
```
But before pushing, we need to make sure that we added everything and committed the changes.

Output:
```sh
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git add README.md 
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git commit -m "Chore: adding readme after part 3 challenge 9"
[master 0c16eb2] Chore: adding readme after part 3 challenge 9
 1 file changed, 54 insertions(+)
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % git push origin master

Counting objects: 6, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 1017 bytes | 1017.00 KiB/s, done.
Total 6 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 2 local objects.
To https://github.com/kardara/Advance_git_Exercise.git
   f5952df..0c16eb2  master -> master
gymubutwari@Ubutwaris-iMac Advance_git_Exercise % 
```

### Challenge 10. 