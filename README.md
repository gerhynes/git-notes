# Git Notes
Sources:
- [The Git and GitHub Bootcamp](https://www.udemy.com/course/git-and-github-bootcamp/)

Git is the world's most popular version control system. Version control is software that tracks and manages changes to files over time.

Version control systems generally allow users to revisit earlier versions of files, compare changes between versions, undo changes, and a whole lot more.

Git is just one of many version control systems available. Other well-known ones include Subversion, CVS, and Mercurial.

They all have similar goals, but vary significantly in how they achieve these goals. Fortunately you likely only need to care about Git because Git is the clear winner. In the 2018 Stack Overflow Developer Survey, nearly 90% of respondents reported Git as their version control system of choice. In 2021, 94% of professional developers reported using Git.

Git helps us:
- Track changes across multiple files
- Compare versions of a project
- "Time travel" back to old versions
- Revert to a previous version
- Collaborate and share changes
- Combine changes

### A Quick History of Git
Linus Torvalds, legendary software engineer, is the the creator and main developer behind Linux and Git.

In 2005, while working on Linux, he became frustrated with the available version control systems. The existing tools were slow, closed-source and usually paid.

Torvalds wanted a version control system that was super fast and free, unlike existing tools.

On 3rd April 2005, he started work on his own VCS, which would become Git. The first official Git release came a few months later. Today, more than 90% of developers worldwide use Git on a daily basis.

### Who uses Git
- Engineers and developers
- Tech-adjacent roles, such as designers
- Governments, for drafting and crowd-sourcing laws and policies
- Scientists, to manage code and data sets
- Writers, such as collaborative writing with multiple authors

### Git vs GitHub
Git is the version control software that runs locally on your machine. You don't need to register for an account. You don't need the internet to use it. You can use Git without ever using GitHub.

GitHub is a service that hosts Git repositories in the cloud and makes it easier to collaborate with other people. You do need to sign up for an account to use GitHub. It's an online place to share work that is done using Git.

### GUI Git Clients vs the Command Line
#### GUI Clients
Pros
- Much lower barrier of entry for beginners compared to the command line
- Can be a better experience (when it works)

Cons
- At times, there is a lot of magic, which obfuscates the inner workings of Git
- Can lead to dependence on a particular piece of software
- When things go seriously wrong, it can be challenging to fix without a command line

#### The Command Line
Pros
- Git is a command-line tool. All the documentation and resources will refer to the command line
- Once you're comfortable, you can be much faster
- Some of the more advanced features are only available on the command line
- The commands are always the same, no matter whcih machine you're working on

Cons
- Not beginner friendly. It can be difficult to learn and remember all the commands at first
- Even for experienced users, it can be a less pleasant experience

Git was designed to run on a Unix-based interface (like Bash). Git Bash is a tool that emulates a Bash experience on a Windows machine.

### Configuring Git
Once you have Git installed on your computer, you need to configure it with your name and email.

Git needs this to know who did what work when making changes and checkpoints.

```bash
git config --global user.name "Your Name"

git config --global user.email yourname@example.com
```

## Git Basics
### Repositories
A Git repository/repo is a workspace which tracks and manages files within a folder.

Any time you want to use Git with a project, you need to create a new git repository. You can have as many repositories on your machine as needed, all with seperate histories and contents.

### `git status`
`git status` gives you information on the current status of a git repository and its contents.

### `git init`
`git init` creates a new Git repository. You need to initialize a repostiory before you can do anything Git-related.

You do this once per project in the top-level folder containing your project.

### The .git Folder
Initializing a Git repository creates a hidden .git folder, containing all your Git history.

Git tracks a directory and all nested subdirectories. Do not initialize a Git repo inside an existing repo. If in doubt, use `git status`.

### The Committing Workflow
The basic Git workflow is
- Work - Make, edit and delete files
- Add - Group specific changes together in preparation for committing
- Commit - Commit everythign that was previously added

The Working Directory is the directory where you initialized the Git repository amd currently work on your project.

The Staging Area is where changes are added to before committing.

The Repository is the `.git` folder itself.

#### `git add`

`git add` adds the files to a staging area.

`git commit` updates the `.git` directory.

You can add multiple files or directories at a time.

```bash
git add file1 file2
```

### `git commit`
`git commit` actually commits changes from the staging area. 

You need to provide a commit message that summarizes the changes.

Running `git commit` by itself will try to use your default editor to add the commit message. The `-m` flag lets you pass in an inline commit message.

```bash
git commit -m "A meaningful commit message"
```

The default editor for Git is Vim. This can however be configured, for example to VS Code:

`git config --global core.editor "code --wait"`

### `git log`
`git log` will print a log of the commits for a given repository. Logs can be formatted for readability. 

Adding the `--oneline` flag will display just the commit's hash and commit message.

`git log --oneline` is shorthand for `git log --pretty=oneline --abbrev-commit`.

### Atomic Commits
When possible, a commit should encompass a single feature, change or fix. In other words, try to keep each commit focused on a single thing.

This makes it much easier to undo or rollback changes later on. It also makes your code easier to review.

### Commit Messages
The Git docs recommend writing commit messages in a present tense imperative style "as if you are giving orders to the codebase to change its behavior".

So "Make...", "Change...", "Fix..."

What matters is consistency, especially when working on a team with many people making commits.

### Amending Commits
Suppose you just made a commit and then realized you forgot to include a file. Or you made a typo in the commit message.

Instead of making a brand new commit, you can "redo" the previous commit with the `--amend` option. This only works for the most recent commit.

This will open the previous commit message in your editor.

```bash
git commit -m "Some commit"
git add forgotten_file.js
git commit --amend
```

### Ignoring Files with `.gitignore`
You can tell Git to ignore specific files and directories in a given repository using a `.gitignore` file.

This is useful for files that you never want to commit, including:
- Secrets, API keys, credentials
- OS files, such as .DS_Store
- Log files
- Dependencies and packages

Inside `.gitignore` you can include:
- exact filenames `.DS_Store`
- entire directories `node_modules/`
- files with a specific extension `*.log`

## Working with Branches
Every commit has a unique identifying hash. Every commit (except for the initial commit) also references at least one parent commit that came before it.

On large projects, multiple team members may be working on the same project at the same time. This work needs to happen in isolation in seperate contexts so that they do not interfere with each other.

Branches are an essential part of Git, creating alternative timelines for a project.

Branches let you create seperate contexts where you can try new tings or even work on multiple ideas in parallel.

If you make changes in one branch, they do not impact the other branches, unless you choose to merge the changes.

### The Default Branch
In Git you are always working on a branch. The default branch name is `master`.

Some people treat the `master` branch as their "source of truth" or the "official branch" for their codebase, but that is left for you to decide.

From Git's perspective, the `master` branch is just like any other branch. It doens't hold the "master copy" of your project.

In 2020 GitHub renamed the default branch from `master` to `main` as part of a broader push to avoid racist language. The default Git branch name is still `master` but the Git team is exploring a potential change.

A common workflow is to have a `main` branch, create feature branches off of it and then merge them back into `main` when that work is completed.

### HEAD
HEAD is a pointer that refers to the current "location" in your repository. It points to a particular branch reference.

By default, HEAD always points to the latest commit you made on the currently checked out branch. But you can move it by changing branch.

### Viewing Branches
Use `git branch` to view your existing branches. The default branch in every Git repo is `master` but this can be configured.

Look for the `*` which indicates the branch you are currently on.

### Creating Branches
Use `git branch branch_name` to make a new branch based on the current HEAD.

This just creates the branch, it doesn't switch you to the branch (the HEAD stays the same).

### Switching Branches
Once you have created a new branch, you can use `git switch branch_name` to switch to it. HEAD will now point to the new branch.

`git switch -c branch_name` will create a new branch and switch to it.

### `git checkout` vs `git switch`
Historically, you used `git checkout branch_name` to switch branches. This still works.

`git checkout -b branch_name` will create a new branch and switch to it.

The `checkout` command does a lot of other things, so the decision was made to add a standalone `switch` command to simplify things.

### Switching Branches with Unstaged Changes
If you try to switch Git branches while you have unstaged changes, you will get an error. 

You have a choice to either commit your work or stash it.

### Deleting and Renaming Branches
Use `git branch -d branch_name` to delete a branch. You can't delete a branch if it's the currently checkout out branch.

If the branch is not fully merged, you will get a warning. You can force delete it using `git branch -D branch_name`.

Use `git branch -m new_branch_name` to rename a branch. You need to be on the branch that you are renaming.

### How Git stores HEAD and Branches
Inside the `.git` directory is a file called `HEAD` that points to the currently checked out branch, such as `refs/heads/main`.

Inside the `refs/heads` directory is a file for every branch. Each of these files contains a Git hash for the latest commit on that branch.

## Merging Branches
Branches make it easy to work within self-contained contexts, but often you'll want to incorporate changes from one branch into another. 

You can do this using the `git merge` command.

There are two main things to remember about merging:
- You merge branches, not specific commits
- You always merge to the current HEAD branch

To merge a branch:
1. Switch to the receiving branch, the branch you want to merge the changes into
2. Use `git merge branch_name` to merge changes from a specific branch into the current branch.

So for example, to merge the `bugfix` branch into `main` use:

```bash
git switch main

git merge bugfix
```

`main` and `bugfix` now point to the same commit until they diverge again. `main` has caught up to the commits on `bugfix` in what is called a **fast-forward merge**.

### Merge Conflicts
Not all merges are fast-forward merges. Often, other people will have added commits to the `main` branch before you are ready to merge.

If there are no conflicts, Git will perform a **merge commit**, resulting in a new commit on the `main` branch. Git will prompt you for a commit message.

Depending on the specific changes you are trying to merge, Git may not be able to automatically merge. This results in **merge conflicts**, whcih you need to manually resolve.

When you encounter a merge conflict, Git warns you in the console that it could not automatically merge.

```bash
CONFLICT(content): Merge conflict in filename.txt
Automatic merge failed; fix conflicts and then commit the result.
```

It also changes the contents of your files to indicate the conflicts that it wnats you to resolve.

```
<<<<<<< HEAD
I have 2 cats
I also have chickens
=======
I used to have a dog :(
>>>>>>> bugfix
```

### Resolving Conflicts
Whenever you encounter merge conflicts, follow these steps to resolve them:
1. Open the file(s) with merge conflicts
2. Edit the file(s) to remove the conflicts. Decide which branch's content you want to keep. Or keep the content from both
3. Remove the conflict markers in the document
4. Add your changes and then make a commit

### Using VS Code to Resolve Conflicts
VS Code has features for dealing with merge conflicts.

You will be given the options to Accept Current Changes, Accept Incoming Changes, Accept Both Changes, or Compare Changes.

## Comparing Changes with Git Diff
You can use `git diff` to view changes between commits, branches, files, the working directory, and more.

You will often use `git diff` alongside commands like `git status` and `git log` to get a better picture of a repository and how it has changed over time.

`git diff`, without additional options, lists all the changes in your working directory that are not staged for the next commit. It compares the staging area and the working directory.

For each comparison, Git explains which files it's comparing. Usually, this is two versions of the same file.

Git also declares one file as "A" and the other as "B".

You really don't need to care about the file metadata. The first two numbers are the hashes of the log files being compared. The last number is an internal file mode identifier.

File A and B are each assigned a symbol.
- A gets a minus sign
- B gets a plus sign

A diff won't show the entire contents of a file, but instead only shows the portions, or "chunks", that were modified.

A chunk also includes some unchanged lines before and after a change to provide some context.

Each chunk starts with a chunk header, found between @@ and @@. This tells you where files were removed from file A and their start line, then where files were added to file B and their start line.

Every line that changed between the two files is marked with either a + or -. Lines that beign with - come from file A, line sthat begin with + come from file B.

### Viewing Unstaged Changes
Without additional options, `git dif` lists all the changes in the working directory that are not staged for the next commit.

### Viewing Working Directory Changes
`git diff HEAD` lists all changes, both staged and unstaged, in the working directory since your last commit.

### Viewing Staged Changes
`git diff --staged` or `git diff --cached` will list the changes between the staging area and your last commit.

It essentially shows you what will be included in the commit if you commit right now.

### Diffing Specific Files
You can view the changes within a specific file by providing `git diff` with a filename.

```bash
git diff HEAD filename

git diff --staged filename
```

### Comparing Changes Across Branches
`git diff branch1 branch2` will list the changes between the tips of the two branches. The two branchnames can be seperated by a space or `..`.

```bash
git diff branch1 branch2

git diff branch1..branch2
```

### Comparing Commits
To compare two commits, provide `git diff` with the commit hashes of the commits in question.

```bash
git diff commit1 commit2
```

## Git Stashing
If you switch from a Git branch that has unstaged changes, one of two things will happen:

1. The changes will come with you to the destination branch
2. Git won't let you switch if it detects potential conflicts

Stashing is an easy way to stash these uncommitted changes so that you can return to them later, without having to make unnecessary commits.

`git stash` helps you save changes that you are not yet ready to commit. You can stash changes and come back to them later.

Running `git stash` (or `git stash save`) will take all uncommitted changes (staged and unstaged) and stash them, reverting the changes in your working copy.

Use `git stash pop` to remove the most recently stashed changes in your stash and reapply them to your working copy.

```bash
git stash
git switch other_branch
# add and commit changes
git switch first_branch
git stash pop
```

### `git stash apply`
You can use `git stash apply` to apply whatever is stashed away, without removing it from the stash. This can be useful if you want to apply stashed changes to multiple branches.

### Working with Multiple Stashes
You can add multiple stashes onto the stack of stashes. They will all be stashed in the order you stashed them.

```bash
git stash
# do other work
git stash
# do other work
git stash
# do other work
```

Git assumes you want to apply the most recent stash when you run `git stash apply`, but you can also specify a particular stash using the stash's id.

```bash
git stash apply stash@{2}
```

### Dropping and Clearing the Stash
To delete a particular stash, you can use `git stash drop stash_id`.

```bash
git stash drop stash@{2}
```

To clear out all stashes, run `git stash clear`.

## Undoing Changes and Time Travelling
### Checking Out Old Commits
You can use `git checkout commit_hash` to view a previous commit.

You can use `git log` to view command hashes. You just need the first seven digits.

You will see that you are in "detached HEAD" state. 

Usually, HEAD points to a specific branch reference rather than a particular commit. The branch reference then points to the last commit made on a particular branch. 

When you make a new commit, the branch reference is updated to reflect the new commit. The HEAD remains the same however because it's pointing at the branch reference. If you switch branches, HEAD points to the new branch reference.

When you checkout a particular commit, HEAD points at that commit rather than at the branch pointer.

### Detached HEAD
When in detached HEAD state, you have a few options:
1. Stay in detached HEAD to examine the contents of the old commit. Poke around, view the files, etc.
2. Leave and go back to wherever you were before - reattache the HEAD
3. Create a new branch and switch to it. You can now make and save changes, since HEAD is no longer detached.

### Referencing Commits Relative to HEAD
`git checkout` supports a slightly older syntax for referencing previous commits relative to a particular commit.

`HEAD~1` refers to the commit before HEAD (parent)
`HEAD~2` refers to 2 commits before HEAD (grandparent)

```bash
git checkout HEAD~1
```

If you want to go back to where you were, you can use `git switch branch_name` to go to a specific branch or `git switch -` to go back to the last branch you were on.

### Discarding Changes
Suppose you've made changes to a file but don't want to keep them. To revert the file back to whatever it looked like when you last committed, you can use:

```bash
git checkout HEAD filename

# or
git checkout -- filename
```

This discards any changes to that file, reverting back to the HEAD.

### Git Restore
`git restore` is a new Git command that helps with undoing operations.

`git restore` was introduced alonsgide `git switch` as an alternative for some of the uses for `git checkout`.

#### Unmodifying Files with Restore

Suppose you've made some changes to a file since your last commit. You've saved the file but then realize you definitely don't want those changes anymore.

To restore the file to the contents in the HEAD, use:

```bash
git restore filename
```

This command is not undoable. If you have uncommited changes in the file, they will be lost.

`git restore filename` restores using HEAD as the default source but you can change that using the `--source` option.

For example, `git restore --source HEAD~1 app.js` will restore the contents of `app.js` to its state from the commit prior to HEAD. You can also use a particular commit hash as the source.

#### Unstaging Files with Restore
If you have accidentally added a file to your staging area with `git add` and you don't want to include it in the next commit, you can use `git restore` to remove it from staging. 

Use the `--staged` otpion.

```bash
git restore --stages filename
```

`git status` will tell you how to use both versions of `git restore`.

### Undoing Commits with Git Reset
Suppose you've just made a couple of commits on the main branch, but you actually meant to make them on a seperate branch instead. To undo those commits, you can use `git reset`.

```bash
git reset commit_hash
```

`git reset commit_hash` will reset the repo back to a specific commit. Those unwanted commits are gone. The changes to the files are however still in your working directory.

If you want to undo both the commits and the actual changes in your files, you can use the `--hard` option.

```bash
git reset --hard commit_hash
```

For example, `git reset --hard HEAD~1` will delete the last commit and its associated changes.

### Reverting Commits with Git Revert
`git revert` is similar to `git reset` in that they both "undo" changes, but they accomplish it in different ways.

```bash
git revert commit_hash
```

`git reset` actually moves the branch pointer backwards, eliminating commits.

`git revert` instead creates a brand new commit which reverses/undoes the changes from a commit. Because it results in a new commit, you will be prompted to enter a commit message.

Reverting a commit can result in conflicts that you will have to resolve.

#### Which Reversing Command to Use?

Both `git reset` and `git revert` help you to reverse changes, but there is a significant difference when it comes to collaboration.

If you want to reverse some commits that other people already have on their machines, you should use `git revert`.

If you want to reverse commits that you haven't shared with other, use `git reset` and no one will ever know.

## GitHub
GitHub is a hosting platform for Git repositories. You can put your repositories on GitHub and access them from anywhere and share them with people around the world.

Beyond hosting repos, GitHub also provides additional collaborative features that are not native to Git but that help people to share and collaborate on repos.

There are many other tools that provide similar hosting and collaborative features, such as GitLab, Bitbucket, and Gerrit. But GitHub is by far the most popular and has become the world's largest host of source code. In early 2020, GitHub reported having over 40 million users and over 190 million repositories on the platform.

GitHub offers its basic service for free. While it does offer paid Team and Enterprise tiers, the basic free tier allows for unlimited public and private repos, unlimited collaborations, and more.

GitHub makes collaboration on a project much easier. Today, GitHub is the home of open source projects on the internet. Projects ranging from React to Swift are hosted on GitHub. If you plan on contributing to open source, you will need to get comfortable working with GitHub.

Your GitHub profile showcases your own projects and contributions to other's projects. It can act as a resumé and you can gain credibility on the platform for creating or contributing to popular open source projects.

Being active on GitHub can help you stay up to date with the projects and tools you rely on, learning about upcoming changes and the decisions/debates behing them.

### Cloning Repos with `git clone`
Cloning is a way to get a local copy of an existing Git repo. All you need is a URL for the remote hosted repo, whether that's GitHub or a similar service.

To clone a repo, use:

```bash
git clone repo_url
```

Git will retrieve all the files associated with the repository and copy them to your local machine.

In addition, Git initializes a new repository on your machine, giving you access to the full Git history of the cloned project.

Make sure you're not inside another repo when you clone.

Anyone can clone a repository from GitHub, provided the repo is public. You don't need to be an owner or collaborator to clone the repo locally to your computer. You just need the URL from GitHub.

Pushing up your changes to GitHub, that's another question.

`git clone` is a standard Git command. It's not tied specifically to GitHub and you can use it with repos hosted anywhere.

### Registering with GitHub and Setting up SSH
It's best if you use the same email for Git and for GitHub

You need to be authenticated on GitHub to do certain operations, like pushing up code from your local machine. Your terminal will prompt you every single time for your GitHub email and password unless you generate and configure an SSH key. Once configured, you can connect to GitHub without having to supply your username or password.

You can check for existing SSH keys using 

```bash
# lists files in your .ssh directory, if they exist
ls -al ~/.ssh
```

Check the directory listing to see if you already have a public SSH key. By default, the filename wof the public keys are one of the following:
- id_rsa.pub
- id_ecdsa.pub
- id_ed25519.pub

### Creating a GitHub Repo
You have two options for creating a project on GitHub

If you already have an existing repo locally, you can:
- Create a new empty repo on GitHub
- Connect your local repo (add a remote)
- Push your changes up to GitHub

If you haven't begun work on a local repo, you can:
- Create a new repo on GitHub
- Clone it down to your local machine
- Do some work locally
- Push your changes up to GitHub

### Git Remote
In Git, remote repositories are accessed via remotes, a destination URL where a hosted repository lives.

Use `git remote -v` to see a remote's name and URL.

To add a new remote, you need to provide a name and URL.

```bash
git remote add name url

git remote add origin https://github.com/username/reponame.git
```

origin is a conventional Git remote name, but is not special. It's just a name for the URL.

When you clone a GitHub repo, the default remote name set up for you is origin. You can change it though most people leave it.

It's not common, but if needed you can rename or delete a remote.

```bash
git remote rename old_name new_name

git remote remove name
```

### Pushing Code to Remote Repos
Once you have a remote set up, you can push code to it using `git push`. You need to specify the remote you want to push to and the specific branch you want to push up to that remote.

```bash
git push remote branch_name
```

So `git push origin main` tells Git to push the main branch up to the origin remote. If a main branch doesn't exist on GitHub, this will create a main branch on GitHub.

While you usually want to push a local branch to a remote branch of the same name, you don't have to.

```bash
git push origin local_branch:remote_branch
```

### The `-u` Option
The `-u` option (equivalent to `--set-upstream`) lets you set the upstream of the branch you're pushing. You can think of this as a link connecting your local branch to a remote branch on GitHub.

Running `git push -u origin main` sets the upstream of the local main branch so that it tracks the main branch on the origin repo.

Once you've set the upstream for a branch, you can us ethe `git push` shorthand which will push the current branch to the upstream.

```bash
git push -u origin main

# next time
git push
```

If you clone a repo from GitHub, it automatically configures the remote for you.

### GitHub Default Branches
If you create a new repo on GitHub with a file in it, it will set main as the default branch. You can change this in the settings.

When you create an empty repo, GitHub encourages you to use `git branch -M main` to rename your default branch to main.

## Fetching and Pulling
### Remote Tracking Branches
When you clone a repo from GitHub, it has two branch references: 
- the standard default branch reference (main)
- a remote tracking branch (origin/main)

The **Remote Tracking Branch** is a reference to the state of the main branch on the remote. You can't movie this yourself. It's like a bookmark poitning to the last known commit on the main branch on origin.

Remote tracking branches tell you: at the time you last communicated with this remote repository, here is where X branch was pointing.

They follow the pattern: remote/branch.
- origin/main references the state of the main branch on the remote repo named origin
- upstream/logo-redesign references the state of the logo-redesign branch on the remote named upstream (a common remote name).

Use `git branch -r` to view the remote branches your local repo knows about.

When you run `git status` you will see whether your local branch is ahead or behind the remote branch.

You can checkout these remote branch pointers. You will go into detached HEAD

```bash
git checkout origin/main
```

### Working with Remote Branches
When you clone a repo with multiple branches from GitHub, you only get access to the main branch in your workspace.

Run `git branch -r` to view the remote branches your local repo knows about. Your repo has a remote tracking reference to any of the other branches in the remote repo.

By default, your main branch is already tracking origin/main. You didn't connect them yourself.

Run `git switch remote_branch_name` to create a new local branch from the remote branch of the same name. For example, `git switch puppies` will make a local puppies branch and set it up to track the remote branch origin/puppies.

### Fetching
Fetching lets you download changes from a remote repo but those changes will not be automatically integrated into your working files.

It lets you see what others have been working on without having to merge those changes into your local repo.

The `git fetch remote` command fetches branches and history from a specific remote repo. It only updates remote tracking branches.

`git fetch origin` will fetch all changes from the origin remote repo. If not specified, remote defaults to origin.

You will now have the changes on your machine but if you want to see them, you have to `checkout origin/main`. Your main branch is untouched.

You can also fetch a specific branch from a remote using `git fetch remote branch_name`. For exmaple, `git fetch origin main` would retrieve the latest information from the main branch on the origin remote repo.

`git fetch`:
- Gets changes from remote branch(es)
- Updates the remote tracking branches with the new changes
- Does not merge changes onto your current HEAD branch
- Safe to do at any time

### Pulling
`git pull` is another command you can use to retrieve changes from a remote repository. Unlike fetch, pull actually updates your HEAD branch with whatever changes are retrieved from the remote.

To pull, you specify the particular remote and branch you want to pull using 

```bash
git pull remote branch_name
```

Just like with `git merge`, it matters where you run this command from. Whatever branch you run it from is where the changes will be merged into.

`git pull origin main` would fetch the latest information from the origin's main branch and merge those changes into your current branch.

Pulls can result in merge conflicts, just like any other merge.

If you run `git pull` without specifying a particular remote or branch to pull from, Git assumes the following:
- remote will default to origin
- branch will default to whatever tracking connection is configured for your current branch

This behaviour can be configured and tracking connections can be changed manually but most people don't change these.

So, if you are on the main branch and run `git pull`, Git will pull from origin/main automatically.

`git pull`:
- Gets changes from remote branch(es)
- Updates the current branch with the new changes, merging them in
- Can result in merge conflicts
- Not recommended if you have uncommitted changes


## GitHub Odds and Ends
### Public and Private Repos
You can make any repo you own public or private on GitHub. 

Public repos are accessible to everyone on the internet. They would still need collaborator permissions to make any changes to the repo.

Private repos are only accessible to the owner and people who have been explicitly granted access.

### Adding Collaborators
You can add collaborators to GitHub repos, giving them the ability to view private repos and push changes. Only the repo owner can change the repo's settings.

### READMEs
A README file is used to communicate important information about a repository, including:
- What the project does
- How to run the project
- Why it's noteworthy
- Who maintains the project

If you put a README in the root of your project, GitHub will recognize it and automatically display it on the repo's homepage.

READMEs are Markdown files. Markdown is a convenient syntax to generate formatted text.

### GitHub Gists
GitHub Gists are a simple way to share code snippets and useful fragments with others. Gists are easier to create but offer far fewer features than a typical GitHub repo.

### GitHub Pages
GitHu Pages are public webpages hosted and published via GitHub. They allow you to create a website simply by pushing your code to GitHub.

It's a hosting service for static webpages and doesn't support serverside code like Node, Python, or Ruby.

GitHub Pages are divided between
- User sites
- Project sites

You get one user site per GitHub account. You could use it to host a portfolio or some other personal website. The default URL is username.github.io, though you can change it.

You get unlimited project sites with each GitHub repo potentially having a corresponding hosted website. You just need to tell GitHub which branch contains the web content. The default URL is username.github,io/repo-name. 

From GitHub's settings, you select a source branch, folder (root or /docs), and optionally a theme.

## Git Collaboration Workflows
### Centralized Workflow
The simplest collaborative workflow is to have everyone work on a single main branch. It's straightforward and can work for some teams but has many shortcomings.

- Lots of time spent resolving conflicts and merging code
- No one can work on anything without disturbing the main codebase
- The only way to collaborate on a feature is to push incomplete code to main

### Feature Branch Workflow
Rather than working directly on main, all new development should be done on separate branches.

- Treat main as the official project history
- Multiple teammates can collaborate on a single feature and share code back and forth without polluting the main branch
- The main branch won't contain broken code

There are controls on merging into main. At the very least there's code review.

At some point new work on feature branches will need to be merged into the main branch.

Your options include:
1. Merge at will, without discussion with teammates
2. Email/dm your team to discuss if the change should be merged
3. Pull Requests

### Pull Requests
Pull Requests are a feature built into products like GitHub and Bitbucket. They are not native to Git itself.

They allow developers to alert team members to new work that needs to be reviewed, provide a mechanism to approve or reject work, and can help facilitate discussion and feedback on the specified commits. 

The typical workflow is:
1. Do some work locally on a feature branch
2. Push up the feature branch to GitHub
3. Open a pull request using the feature branch that was just pushed to GitHub
4. Wait for the PR to be approved and merged. Possibly start a discussion on the PR. This depends on the team structure

### Merging Pull Requests with Conflicts
If there is a merge conflict on a PR, GitHub will give you the option to resolve the conflict in the browser or via the command line.

```bash
# Bring changes into your project repository
git fetch origin
git switch branch_name
git merge main

# Fix the conflict

# Merge the changes and update on GitHub
git switch main
git merge branch_name
git push origin main
```

### Branch Protection Rules
You can define branch protection rules to disable force pushing, prevent branches from being deleted, and optionally require status checks before merging.

You can apply rules to branches via a name pattern, such as `/feature/` or `/release/`.

You can
- require pull request reviews before merging
- require status checks to pass before merging
- require signed commits
- require linear history
- allow/deny force pushes
- allow/deny branch deletions

### Forking and Cloning Workflow
GitHub, and similar tools, allow you to create personal copies, or forks, of other peoples' repositories. 

When you fork a repo, you're essentially asking GitHub to make you your own copy of the repo.

As with pull requests, forking is not a Git feature. The ability to fork is implemented by GitHub.

The fork and clone workflow is different from the above workflows. Instead of one centralized GitHu repo, every developer has their own GitHub repo in addition to the main repo.

Developers make changes and push to their own forks before making pull requests.

It's commonly used on large scale open-source projects where there may be thousands of contributors but only a couple of maintainers.

You can clone your fork, make changes, and push them back up to your fork.

Once you've made changes to your fork, you can open a pull request against the original repo.

When you clone a repo, Git automatically adds a remote called origin that points to your forked repo on GitHub. You can add a remote pointing to the original repo (not the fork). This remote can be named anything but you'll often see upstream or original. This allows you to pull changes from the original repo while also pushing your changes to your fork.

You don't have permissions to push to upstream but you can push to origin.

The workflow involves:
1. Fork the project
2. Clone the fork
3. Add upstream remote
4. Do some work
5. Push to origin
6. Open PR


## Rebasing
There are two main ways to use the `git rebase` command:
- as an alternative to merging
- as a cleanup tool

Instad of merging the main branch into a feature branch to bring it up to date, you can use `git rebase` to rebase the feature branch onto the main branch. This moves the entire feature branch so that it begins at the tip of the main branch. All of the work is still there but you have re-written history.

Instead of using a merge commit, rebasing rewrites history by creating new commits for each of the original feature branch commits.

You can also wait until you're all done with a feature and then rebase the feature branch onto the main branch.

```bash
git switch feature_branch

git rebase main
```

Just like with merging, rebasing can result in merge conflicts which need to be resolved.

### When Not to Rebase
Rebasing produces a much cleaner, liner project history with no unnecessary merge commits.

Never rebase commits that have been shared with others. If you have already pushed commits up to GitHub, do not rebase them unless you are positive no one on the team is using those commits.

## Interactive Rebasing
Sometimes you might want to rewrite, delete, rename, or reorder commits (before sharing them). You can do this using `git rebase`.

Running `git rebase` with the `-i` option will enter interactive mode, which allows you to edit commits, add files, drop commits. You need to specify how far back you want to rewrite commits.

In this case you are not rebasing another branch, you are rebasing a series of commits onto the HEAD they are currently based on.

```bash
git rebase -i HEAD~4
```

In your editor, you'll see a list of commits in reverse chronological order alongside a list of commands that you can choose from.

The more commonly used commands are:
- pick - use the commit
- reword - use the commit but edit the commit message
- edit - use the commit but stop for amending
- fixup - use the commit's contents but meld it into the previous commit and disacrd the commit message
- drop - remove the commit

When you close your editor, Git will run the commands you selected. 

If you change a commit, it and every commit after it will be rewritten, resulting in new commit hashes.

## Git Tags
Tags are pointers that refer to particular points in Git history. You can mark a particular point in a repo's history as being important with a tag. Tags are most often used to mark version releases in projects, such as 4.1.0, 4.1.1.

Think of tags as branch references that do not change. Once a tag is created, it always refers to the same commit. It's a label for that commit.

There are two types of Git tags:
- **lightweight tags** - lightweight, a name/label that points to a particular commit
- **annotated tags** - store extra metadata including the author's name and email, the date, and a tagging message (like a commit message)

### Semantic Versioning
The semantic versioning spec outlines a standardized versioning system for software releases. It provides a consistent way for developers to give meaning to their software release, such as how big a change a release was.

Versions consist of three numbers, such as 2.4.1, for major releases, minor releases and patch releases.

The initial public-facing release will be 1.0.0. 

**Patch releases** (1.0.1) normally do not contain new features or significant changes. They typically signify bugfixes and other changes that do not impact how the code is used.

**Minor releases** (1.1.0) signify that a new feature or functionality have been added, but the project is still backwards compatible. No breaking changes. The new functionality is optional and should not force users to rewrite their own code. The patch number is reset.

**Major releases** (2.0.0) signify significant changes that are no longer backwards compatible. Features may be removed or changed substantially.

A pre-release version can have extra details appended, such as `-beta.1`.

### Viewing and Searching Tags
`git tag` will print a list of all the tags in the current repository.

You can search for tags that match a particular pattern by using `git tag -l` and then passing a wildcard pattern. For example, `git tag -l "*beta*"` will print a list of tags that include "beta" in their name.

To view the state of a repo at a particular tag, you can use `git checkout tag`. This will put you in detached HEAD.

You can compare tagged commits using `git diff`.

```bash
git diff v16.14.0 v17.0.0
```

### Creating Lightweight Tags
Use `git tag tagname` to create a lightweight tag. By default, Git will create the tag referring to the commit that HEAD is referencing.

### Creating Annotated Tags
Use `git tag -a tagname` to create an annotated tag. Git will then open your default text editor and prompt you for additional information.

Similar to `git commit` you can also use the `-m` option to pass a message directly and forgo opening the editor.

### Tagging Previous Commits
You can also tag an older commit by providing the commit hash.

```bash
git tag tagname commit_hash
```

### Replacing Tags
If you make a mistake and want to apply a tag to a different commit, you need to use the `-f` flag to force it. The tag will then refer to the updated commit.

```bash
git tag tagname commit_hash -f
```

### Deleting Tags
Use `git tag -d tagname` to delete a tag.

### Pushing Tags
By default, the `git push` command doesn't transfer tags to remote servers. If you have several tags that you want to push up at once, you can use the `--tags` option. This will transfer all of your tags to the remote server that are not already there.

```bash
git pus --tags
```

You can also push a single tag.

```bash
git push origin tagname
```

## Git Behind the Scenes
### Working With the Local Config File
You can configure global settings like your name and email across all Git repos, but you can also configure things on a per-repo basis using the config file which is located in every .git folder. 

You can use `git config --local` to set local configuration properties.

```bash
git config --local color.ui true
```

### Refs Folder
Inside of refs, you'll find a heads directory. `ref/heads` contains one file per branch in a repository. Each file is named after a branch and contains the hash of the commit at the tip of the branch.

For example, `ref/heads/main` contains the commit hash of the last commit on the main branch.

Refs also contains a `refs/tags` folder which contains one file for each tag in a repo.

### The HEAD file
HEAD is a text file that keeps track of where HEAD points.

If it contains `ref: refs/heads/main`, this means that HEAD is pointing to the main branch.

In detached HEAD, the HEAD file contains a commit hash instead of a branch reference.

### The Objects Folder
The objects directory contains all the repo files. This is where Git stores the backups of files, the commits in a repo, and more. The files are all compressed and encrypted.

Inside this folder are four types of Git objects:
- commits
- trees
- blobs
- annotated tags

### Hashing Functions
Hashing functions are functions that map input data of some arbitrary size to fixed-size output values.

Cryptographic hash functions are a subset with additional constraints:
1. One-way function which is infeasible to invert
2. Small change in the input yields large change in the output
3. Deterministic - same input yields same output
4. Unlikely to find two outputs with the same value

Git uses the SHA-1 hashing function (though this is planned to eventually change). SHA-1 always generates 40-digit hexadecimal numbers, which Git uses for commit hashes.

### Git as a Key-Value Data Store
Git is a key-value data store. You can insert any kind of content into a Git repository and Git will hand back a unique key you can later use to retrieve that content. The keys that you get back are SHA-1 checksums.

Giving Git the key allows you to retrieve the value associated with it.

### Hashing With `git hash-object` 
The `git hash-object` command takes some data, stores it in your `.git/objects` directory, and gives you back the unique SHA-1 hash that refers to that data object.

In its simplest form, Git simply takes some content and returns the unique key that would be used to store the object. But it does not actually store anything.

```bash
git hash-object filename
```


The `--stdin` option tells git hash-object to use the content from stdin rather than a file. 

```bash
echo 'hello' | git hash-object --stdin
```

Rather than simply outputting the key that Git would store the object under, you can use the `-w` option to tell Git to actually write the object to the datastore in `.git/objects`. 

It will create a folder named with the first two characters of the hash, and then a file named with the other 38 characters.

```bash
echo 'hello' | git hash-object --stdin -w
```

### Retrieving Data With `git cat-file`
Once you have data stored in a Git object datastore, you can retrieve it using the `git cat-file` command. The `-p` options tells Git to pretty print the contents of the object based on its type.

```bash
git cat-file -p object_name
```

### Blobs
Git blobs (binary large objects) are the oject type Git uses to store the contents of files in a given repository. Blobs don't even include the filenames of each file or any other dat. They just store the contents of a file.

Blobs get their own hash, output by the same SHA-1 function.

### Trees
Trees are Git objects used to store the contents of a directory. Each tree contains pointers that can refer to blobs and to other trees.

Each entry in a tree contains the SHA-1 hash of a blob or tree, as well as the mode, type, and filename.

You can use the `git cat-file` command with `main^{tree}` to specify the tree object that is pointed to by the tip of the main branch.

```bash
git cat-file -p main^{tree}
```

### Commits
Commit objects combine a tree object along with information about the context that led to the current tree. 

Commits store a reference to parent commit(s), the authro, the commiter, and the commit message.

When you run `git commit`, Git creates a new commit object whose parent is the current HEAD commit and whose tree is the current content of the staging area.

## Retrieving Lost Work
### Reflogs
Git keeps a record of when the tips of branches and other references were updated in the repo.

You can view and update these reference logs using the `git reflog` command.

In the `.git` directory, there is a `logs` directory. Inside `logs` is a `HEAD` file containing entries for every time you update the HEAD reference, such as by switching branches. 

Git only keeps reflogs on your local activity. They are not shared with collaborators. Reflogs also expire. Git cleans out old entries after about 90 days, though this can be configured.

### `git reflog`
The `git reflog` command accepts subcommands `show`, `expire`, `delete`, and `exists`. Show is the only commonly used variant, and is the default subcommand.

`git reflog show` will show the log of a specific reference (it defaults to HEAD). For example, to view the logs for the tip of the main branch, you could run

```bash
git reflog show main
```

### Reflog References
You can access specific Git refs using `name@{qualifier}`.  This syntax lets you access specific ref pointers and pass them to other commands, including `checkout`, `reset`, and `merge`.

### Time-Based Reflog Qualifiers
Every entry in the reflogs has a timestamp associated with it. You can filter reflogs entries by time/date by using time qualifiers like:
- 1.day.ago
- 3.minutes.ago
- yesterday
- Fri, 12 Feb 2021 14:06:21-0800

```bash
git reflog main@{one.week.ago}

git checkout bugfix@{2.days.ago}

git diff main@{0} main@{yesterday}
```

### Rescuing Lost Commits With Reflog
You can sometimes use reflog entries to access commits that seem lost and are not appearing in the Git log.

If you undo a commit using `git reset --hard`, it will not be available in the Git log but that information is still available in the reflog (until the reflog gets cleared). 

```bash
# view reflog
git reflog show main

# access previously lost commit
git reset --hard _lost_commit_hash
```

### Undoing a Rebase With Reflog
Reflog can recover changes lost because of a rebase.

```bash
git rebase -i HEAD~4

# all commits still visible
git reflog show branch_name

# access previously lost commit
git reset --hard _lost_commit_hash
```

## Git Aliases
### Global Git Config
Git looks for the global config file at either `~/.gitconfig` or `~/.config/git/config`. Any configuration variables that you change in the file will be applied across all Git repos.

```
[user]
        email = yourname@example.com
        name = yourname
[core] 
				editor = code --wait
[alias]
        new = !git init && git symbolic-ref HEAD refs/heads/main
[init]
        defaultBranch = main
```

You can also alter configuration variables from the command line if you prefer.

```bash
git config --global user.name username
```

You can set up aliases to make your Git experience a bit simpler and faster. For example, you could set `git lg` to print a custom formatted commit log. 

Git will automatially pass arguments to aliases.

```
[alias]
			s = status
			lg = log --oneline
```

```bash
git config --global alias.showbranches branch
```

An `!` in a Git alias tells Git that it is a shell script. These need to include `git` in the command.

```
# list all git aliases
la = "!git config -l | grep alias | cut -c 7-"
```

When working with others, bear in mind they won't use all the same aliases as you.