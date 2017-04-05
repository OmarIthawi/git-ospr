# Git OpenSource Commands
Git commands for painless opensource pull request (OSPR) contributions.

**WARNING:** This repo does a lot of
[git history rewriting](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History).
Things could break! Your work might get lost. Use at your own risk.
Seriously!

## Setup
Before your try to set this up, note that this repo is opinionated about a few
things. Let's agree on them first:

 - the `ospr-*` commands don't care about the `origin` repo,
   though it can play nicely with it.
 - You need one `upstream` repo for example:
   https://github.com/edx/edx-platform.git
 - and another one called `ospr` for example:
   https://github.com/OmarIthawi/edx-platform.git
 - A local branch named `upstream-master` that is linked to the remote
   branch `upstream/master`. Therefore your `ospr/master` won't be used.

If you don't like the naming and want some change, please open an issue.
Or just fork the repo and change it.

### Installing Steps
To install the commands do the following:

```
$ cd ~
$ git clone https://github.com/OmarIthawi/git-ospr.git
$ mkdir -p ~/.config/git/
$ ln -s ~/git-ospr/config ~/.config/git/config
```

To ensure it is installed, run the following command:
```
$ cd path/to/any/git/repo
$ git branch-name
```

It should print the branch name.

#### Configuring a Repo
Unlike the installation above, this has to be done on each repo.

Replace the `git@github.com:*` with your desired repos.

```
$ git remote add upstream git@github.com:edx/edx-platform.git
$ git remote add ospr git@github.com:OmarIthawi/edx-platform.git
$ git fetch --all
$ git checkout -b upstream-master upstream/master
$ git ospr-check && echo "Everything is setup correctly"
```

## Commands
Those are the main commands I use during the open-source pull requests:

 - `$ git ospr-nbr BRANCH_NAME`: Creates an OSPR (open-source
   pull request) branch with proper base and pushes it to the correct remote.
 - `$ git ospr-rebase`: Rebases the branch with the upstream-master. Accepts extra rebase arguments like `--interactive`
   and others.
 - `$ git ospr-fetch-rebase`: Updates `upstream-master` and continue with `$ git ospr-rebase`. Accepts extra rebase arguments like `--interactive`
   and others.
 - `$ git ospr-diff`: Diff with upstream/master.

## Extra Commands
The commands above wouldn't be possible without adding few other commands
for sanity checks and other things.

  - `$ git branch-name`: Prints the branch name. Useful for other commands

  - `$ git branch-remote`: Prints the remote branch of the current local branch.

  - `$ git ensure-arg ARG`: Ensures that the first argument exists.
    Useful to check command runs.

  - `$ git pull-other BRANCH_NAME`: Pulls another branch, safely.
    Useful before rebasing.

  - `$ git ensure-clean`: Ensures a clean repo before doing anything stupid!

  - `$ git rebase-master`: Pull the base branch `master` and then rebase.
    Accepts extra rebase arguments like `--interactive`.

  - `$ git diff-remote`: Diff with the remote branch, useful before
    `push --force`. Accepts extra diff arguments.

  - `$ git ospr-check-remote REMOTE_NAME`: Checks for the existence specific
    remote. Useful to test the repo before running `ospr-*` commands.

  - `$ git ospr-check`: Checks for both `upstream` and `ospr` remote repos.

  - `$ git ospr-check-ospr-branch`: Verifies that the current branch is an
    OSPR branch with correct setup.

## Why
I work at @Edraak and part of my job is to make opensource pull request
contributions to the [edx-platform](https://github.com/edx/edx-platform) repo.

As a non-member contributor I have to work with three different repositories:

 - [Edraak's fork](https://github.com/Edraak/edx-platform) for @Edraak.
 - The [upstream repo](https://github.com/edx/edx-platform) at @edX.
 - The ["personal" repo](https://github.com/OmarIthawi/edx-platform)
   for opening pull requests against upstream.

This involves a lot of juggling, which is not so much fun and waists a
lot of time in jumping from one git command to another.

I made these commands to help me.

## TODO
Because every project has to have TODO list that will never be done! Here's
mine 😄:

 - [x] Do nothing, sleep and go to work.
 - [ ] Add tests, TravisCI and Coveralls.io integration just because it's
   the cool new thing to do.
 - [ ] Refactor into proper git commands instead of hackish aliases.
 - [ ] Add a setup script for Linux, Mac OSX, Windows, Android and every
   other OS in the galaxy.
 - [ ] Write a book.
 - [ ] Create a MOOC on Coursera, charge 140$ per enrollment and
   become a millionaire.
 - [ ] Create a better version management tool than git.


## Author

 - Omar Al-Ithawi <i@omardo.com>
