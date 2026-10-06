# Git & Github

## Setup & Config

* Global configurations (stored in `~/.gitconfig`)

    > ```sh
    > git config --global user.name "Your Name"
    > git config --global user.email "you@example.com"
    > git config --list # View current configuration
    > ```

* Local configuration (stored in repo's `.git/config`)

    > ```sh
    > git config user.name "Your Name"
    > git config user.email "you@example.com"
    > ```

* Git credentials

    > ```sh
    > vim ~/.git-credentials
    > git config --global credential.helper store # to save git credentials
    > ```

* Alias definition

    > ```sh
    > git config --global alias.tree "log --graph --oneline --all --decorate"
    > git tree
    > ```


## Repository Management

* Repository Creation 

    > ```sh
    > git init                          # Initialize a new local repo
    > git clone <url>                   # Clone an existing remote repo
    > ```

* In Git, the environment relies on three main local areas: the **Working Directory** (where you edit files), the **Staging Area or index** (the preparation zone), and the **Repository** (where committed snapshots live).

* Running `git add <file>` takes either of two cases (**unstaged changes** and **untracked files**) and moves them safely into the staged area, ready for your next commit.

* All new files become **tracked** the moment you run `git add`. When Git is **tracking** a file, it means Git is actively watching that file for any changes, additions, or deletions, and is ready to record its history.

* A **commit hash** is a unique 40-character fingerprint that Git automatically assigns to every single commit you make. Abbreviated hash (shorted commit hash) is showed when you use `git log --oneline`.

* Staging and Committing

    > ```sh
    > git status                        # Check working tree status
    > git add <file>                    # "Stage" a specific file
    > git add .                         # "Stage" all changes
    > git commit -m "commit message"    # "Commit" staged changes
    > git log -1 --oneline              # "-1" means last/latest commit 
    > git log --oneline --graph         # View concise commit history
    > git diff                          # View unstaged changes
    > git diff --staged                 # View staged changes
    > ```

* Checking Current Git State

    > ```sh
    > git status                        # Check working tree status
    > git log -1 --oneline              # "-1" means last/latest commit 
    > git log --oneline --graph         # View concise commit history
    > git diff                          # View unstaged changes
    > git diff --staged                 # View staged changes
    > ```

* **Branch & Merging**

    > ```sh
    > git branch --all                  # List local branches
    > git branch <branch-name>          # Create a new branch
    > git switch <branch-name>          # Switch branches (or: git checkout <branch>)
    > git switch -c <branch-name>       # Create and switch to new branch
    > git merge <branch-name>           # Merge specified branch into current branch
    > git switch --orphan <branch-name> # switch to new orphan branch
    > git branch -d <branch-name>       # (safe) Delete a merged branch
    > git branch -D <branch-name>       # (force) Delete a branch even it remains as unmerged
    > git push origin --delete <branch-name> # delete remote branch
    > git branch -m <new-name>          # Rename a branch
    > ```

* Lifetime of a branch is often considered as temporary. Usually deleted after the feature is merged.

* **Tagging.** Use annotated tags (`-a`) to mark fixed milestones (e.g., paper submissions or releases). Unlike any git branch which is dynamic, the tag is static in nature, it stays fixed to the exact commit where you created it. `<tag-name>` are often formatted as `<name>v<major>.<minor>.<patch>`, such `ACLv1.0.1`. Often related to "Semantic Versioning".

    > ```sh
    > git tag -a <tag-name> -m "CVPR submission code snapshot" # Create an annotated tag on your current commit
    > git push origin <tag-name> # Push the tag to GitHub 
    > git push origin --tags # Push all local tags at once
    > git tag -n # Verify tag exists
    > git switch --detach <tag-name> # Inspect a tag (Detached HEAD)
    > git switch -c <new-branch-name> <tag-name> # Switch to a tag and start working (Create a branch)
    > ```

* **Revert vs Reset.** `git revert` undoes a specific commit by creating a new "anti-commit" (preserving history). `git reset` is a complete rollback that moves your branch backward to an older commit (rewriting history).

    > ```sh
    > # commit-hash before: [A] -> [B (Buggy)] -> [C] -> [D]
    > # commit-hash after: [A] -> [B (Buggy)] -> [C] -> [D] -> [E (Anti-B Commit)]
    > git revert [B]
    > git reset --hard [A] # [dangerous] Delete intermediate commits
    > git reset [A]
    > ```

* **Untracking.** Files 

    > ```sh
    > git rm --cached <file>
    > git rm -r <file> # Deleted without caching
    > git rm -r --cached <dir>
    > git rm -r <dir> 
    > ```

* **Rebase**

    > ```sh
    > git rebase <branch-name>    # rebase current branch in <branch-name>
    > ```

## Remote Management

* **Remote Checking**

    > ```sh
    > git remote -v                     # List remote repositories
    > git remote add origin <url>       # Link local repo to remote
    > ```

* **Fetching**: `git fetch <remote> <branch>`

    > ```sh
    > git fetch origin <branch>         # Download changes without merging
    > ```

* **Pulling (merge)** ~ `git pull origin <branch>`

    > ```sh
    > git fetch origin <branch>
    > git merge origin/<branch>
    > ```

* **Pulling (rebased)** ~ `git pull --rebase origin <branch>`

    > ```sh
    > git fetch origin <branch>
    > git rebase origin/<branch>
    > ```

* **push**

    > ```sh
    > git push origin <branch>          # Push local commits to remote
    > git push -f origin <branch>       # [force] Push local commits to remote
    > git push -u origin main           # Push and set upstream tracking
    > ```

## Github Actions with Workflow 

* Several GitHub Actions (are defined in `.github/workflows/`), automate various tasks across the repository, including continuous integration, documentation, maintenance, and other workflows. Please refer to these workflows on GitHub for details on their purpose and implementation.
