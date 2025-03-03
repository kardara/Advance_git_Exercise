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
