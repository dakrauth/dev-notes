===
git
===

Common git commands
===================

Config
------

Set your details::

    git config --global user.name "John Doe"
    git config --global user.email "john@example.com"

See your settings::

    git config --list


Use `--global` to set the configuration for all projects.
If git config is used without `--global` and run inside a project directory, the settings are set for the specific project.

Add remote::

    git remote add remote-name https://github.com/user/repo.git

Diff
----

See staged, non-commited changes::

    git diff --cached

See differences between local changes and master::

    git diff origin/master

Note that origin/master is one local branch, a shorthand for refs/remotes/origin/master, which is the full name of the remote-tracking branch.

See differences between two commits::

    git diff COMMIT1_ID COMMIT2_ID

See the files changed between two commits::

    git diff --name-only COMMIT1_ID COMMIT2_ID

See the files changed in a specific commit::

    git diff-tree --no-commit-id --name-only -r COMMIT_ID

*or*::

    git show --pretty="format:" --name-only COMMIT_ID

See diff before push::

    git diff --cached origin/master

Compare commits on two branches::

    git diff BRANCH1..BRANCH2

See differences between the current state and a branch::

    git diff branch-name

See differences in a file, between the current state and a branch::

    git diff branch-name path/to/file

Reset
-----

Undo the last local commit::

    git reset --soft HEAD^

Undo last commit, preserving local changes::

    git reset --soft HEAD~1

Undo last commit, without preserving local changes::

    git reset --hard HEAD~1

Undo last commit, preserving local changes in index::

    git reset --mixed HEAD~1

*or*::

    git reset HEAD~1

Undo non-pushed commits::

    git reset origin/master

Reset to remote state::

    git fetch origin
    git reset --hard origin/master


Tags
----

Create a tag::

    git tag 7.x-1.3

Push a tag::

    git push origin 7.x-1.3

Tag and share a release::

    git tag -a release/1.0.0b1 -m "1.0.0b1 release"
    git push --tags
    git show-ref --tags 1.0.0b1

Stash only unstaged files::
    
    git stash save --keep-index

Stage all files, included deletions::

    git add -u

Revert a commit

*If a commit has already been shared publicly, this creates a changeset that reverses the commit.*::

    git revert COMMITHASH

Undo a merge::
    
    git merge --abort

View the url of a remote repository::
    
    git remote -v

or::
    
    git remote show origin

Show the current branch name::
    
    git rev-parse --abbrev-ref HEAD

Push a local branch::
    
    git push origin BRANCH

List remote branches::
    
    git branch -r

*(or -a for all branches)*

Delete a remote branch::

    git push origin :BRANCH

Delete local tracking branches

*Fixes a common error about deleting a branch from origin when another user has already deleted that remote branch.*::
    
    git fetch -p origin

Compare commit messages on two branches::

    git log --cherry-mark --oneline BRANCH1..BRANCH2

Show non-pushed commits::

    git log origin/master..HEAD

*or*::

    git diff origin/master..HEAD

Delete a tag

**Dangerous** This rewrites the public repository and breaks other users’ clones if they have already pulled this tag.::
    
    git tag -d 12345
    git push origin :refs/tags/12345

Move commits to a new branch.

**Dangerous!** You will lose uncommitted work. Only works for moving commits to a new branch.
Moves all commits not on BRANCHNAME to NEWBRANCHNAME.::
    
    git branch NEWBRANCH
    git reset --hard origin/BRANCH
    git checkout NEWBRANCH

Delete untracked files.

**Dangerous!** This permanently deletes untracked files.  But the -n flag does a dry-run to help catch mistakes.::
    
    git clean -fn

Remove from repository all locally deleted files::

    git rm $(git ls-files --deleted)

Delete all untracked files::

    git clean -f

Including directories::

    git clean -n -f -d

Delete all files from a git repository that have already been deleted from disk::

    git ls-files --deleted -z | xargs -0 git rm


Stashing files
--------------

Git stash is a very useful command, where git will 'hide' the changes on a dirty directory - but no worries you can re-apply them later. The command will save your local changes away and revert the working directory to match the HEAD commit.

Stash local changes::

    git stash

Stash local changes with a custom message::

    git stash save "this is your custom message"

Re-apply the changes you saved in your latest stash::

    git stash apply

Re-apply the changes you saved in a given stash number::

    git stash apply stash@{stash_number}

Drops any stash by its number::

    git stash drop stash@{0}

Apply the stash and then immediately drop it from your stack::

    git stash pop

'Release' a particular stash from your list of stashes::

    git stash pop stash@{stash_number}

List all stashes::

    git stash list

Show the latest stash changes::

    git stash show

See diff details of a given stash number::

    git diff stash@{0}

Branching and merging
---------------------

Creating a local branch::

    git checkout -b branchname

Switching between 2 branches (in fact, this would work on terminal as well to switch between 2 directories - $ cd -)::

    git checkout -

Pushing local branch to remote::

    git push -u origin branchname

Deleting a local branch - this won't let you delete a branch that hasn't been merged yet::

    git branch -d branchname

Deleting a local branch - this WILL delete a branch even if it hasn't been merged yet!::

    git branch -D branchname

Remove any remote refs you have locally that have been removed from your remote (you can substitute <origin> to any remote branch)::

    git remote prune origin

Viewing all branches, including local and remote branches::

    git branch -a

Viewing all branches that have been merged into your current branch, including local and remote::

    git branch -a --merged

Viewing all branches that haven't been merged into your current branch, including local and remote::

    git branch -a --no-merged

Viewing local branches::

    git branch

Viewing remote branches::

    git branch -r

Rebase master branch into local branch::

    git rebase origin/master

Pushing local branch after rebasing master into local branch::

    git push origin +branchname


Committing files
----------------

Commit staged file(s)::

    git commit -m 'commit message'

Add file and commit::

    git commit filename -m 'commit message'

Add file and commit staged file::

    git commit -am 'insert commit message'

Amending a commit::

    git commit --amend 'new commit message' or no message to maintain previous message

Squashing commits together::

    git rebase -i

This will give you an interface on your core editor::

    #  p, pick = use commit
    #  r, reword = use commit, but edit the commit message
    #  e, edit = use commit, but stop for amending
    #  s, squash = use commit, but meld into previous commit
    #  f, fixup = like "squash", but discard this commit's log message
    #  x, exec = run command (the rest of the line) using shell

Squashing commits together using reset --soft::

    git reset --soft HEAD~number_of_commits
    git commit

**WARNING:** this will require force pushing commits, which is OK if this is on a branch before you push to master or create a Pull Request.

Resetting
---------

Mixes your head with a give SHA. This lets you do things like split a commit::

    git reset --mixed [sha]

Upstream master::

    git reset HEAD origin/master -- filename

The version from the most recent commit::

    git reset HEAD -- filename

The version before the most recent commit::

    git reset HEAD^ -- filename

Move head to specific commit::

    git reset --hard sha

Reset the staging area and the working directory to match the most recent commit. In addition to unstaging changes, the --hard flag tells Git to overwrite all changes in the working directory, too.::

    git reset --hard

*or*::

    git reset --hard HEAD~1

Reset, but preserve local changes::

    git reset --soft HEAD~1


Git blame
---------

Show alteration history of a file with the name of the author::

    git blame [filename]

Show alteration history of a file with the name of the author && SHA::

    git blame [filename] -l


