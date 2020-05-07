<!-- omit in toc -->
# Git Usage

A reference document for commonly used git commands, as well as general git advice.

- [1. Set up an SSH key](#1-set-up-an-ssh-key)
- [2. Git Commands](#2-git-commands)
  - [2.1 Command ```git log```](#21-command-git-log)
    - [2.2 A note about rewriting history](#22-a-note-about-rewriting-history)
  - [2.3 Command ```git rebase```](#23-command-git-rebase)
  - [2.3 Command ```git reset```](#23-command-git-reset)
  - [2.4 Soft resets](#24-soft-resets)
  - [2.5 Hard resets](#25-hard-resets)
  - [2.6 Command ```git squash```](#26-command-git-squash)
  - [2.7 Command ```git cherry-pick```](#27-command-git-cherry-pick)
  - [2.8 Force push](#28-force-push)
  - [2.9 Force pull](#29-force-pull)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 1. Set up an SSH key

This will make it so you don't have constantly have to retype in your password when you use git. See
following links for instructions:

1. [Generating an SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

2. [Adding SSH key to your Github account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

## 2. Git Commands

Explanation of useful git commands.

### 2.1 Command ```git log```

Shows all commits on your current branch. Note the hashes next to each commit, those are unique to
each commit and identifies each commit.

#### 2.2 A note about rewriting history

When you do anything on git beyond adding commits, you are rewriting history (e.g., removing
commits, force pushing, squashing). Generally, you should never do this on a branch that multiple
people are using, or at least you should let them know, lest ye risk some serious git headaches.

### 2.3 Command ```git rebase```

Imagine you forked your branch from master at commit E, like below

```txt
          A---B---C yourBranch
         /
    D---E---F---G master
```

Master has had additional commits since yours, so you want to rebase (pull in the latest master
commits and then apply your commits on top)

```txt
                  A'--B'--C' yourBranch
                 /
    D---E---F---G master
```

You can do this by running `git rebase master yourBranch`, or in other words,
`git rebase <branch to pull in> <branch with your changes>`

Alternatively, while on your branch you can run `git pull --rebase origin master`. It does the same
thing, it's just a different syntax.

This command will apply your commits one at a time. If there are any merge conflicts, you will need
to resolve them, `git add` whatever file had the conflict, and then run `git rebase --continue` (or
--skip in certain situations).

Whenever possible, rebase your branch before opening a PR to make sure that merges are as clean as
possible. Doing things like running `git pull origin master` without rebasing can cause commits to
be reapplied and can pollute your commit history.

Sometime rebases are impractical, like if you forked your branch a long time ago, you may have to
resolve MANY merge conflicts that are old. In cases like this, it's acceptable to just do a merge
commit, but try not to let your branches get to that point. Consider rebasing regularly if you work
on a branch that has been forked a long time ago.

### 2.3 Command ```git reset```

Git reset comes in two flavors, hard and soft.

Take a list of commits like this, in reverse chronological order (latest commit appears at the top).

```txt
Commit 5: d4166aed7c15b586f2a0b5f0c6c1d9a1056bdef3
Commit 4: b191b0b7581e99ab0c1e1bfe050a892ea91d7455
Commit 3: 623b68e9c1c7bea9945fafc88ece8b7d5be7b6c4
Commit 2: 0120e2c7b01a2e4b6618d2d2e2449b53c2369120
Commit 1: e89084bbb16bf608580fe454cc78dd1e96d5cbae
```

### 2.4 Soft resets

Soft resets revert to the given commit, and unstage any changes that were made by later commits. So
if you ran `git reset 623b68e9c1c7bea9945fafc88ece8b7d5be7b6c4`, then you would revert to commit 3,
and any changes made by commits 4 or 5 would still be present, but would be unstaged. You can then
do something like create a new commit to override them.

### 2.5 Hard resets

Hard resets revert to the given commit and remove any changes that were made by later commits. If
you run `git reset --hard 623b68e9c1c7bea9945fafc88ece8b7d5be7b6c4`, then you would revert to commit
3 and any changes in commits 4 or 5 will be removed completely. **Be careful with this, you can lose
work doing this**

### 2.6 Command ```git squash```

The soft reset, commit trick earlier is one way of squashing commits. Here's another way using
`git rebase`.

Let's say you want to squish your last 4 commits into a single one. Run `git rebase -i HEAD~4`,
you'll get this in response.

```txt
$ git rebase -i HEAD~4

pick 01d1124 Monday commit
pick 6340aaa Tuesday commit
pick ebfd367 Wednesday commit
pick 30e0ccb Thursday commit
```

Note that this list is in chronological order (the opposite order of your `git log`).

To squish Tuesday into Monday, you want to change `pick` into `fixup`

```txt
pick 01d1124 Monday commit
fixup 6340aaa Tuesday commit
pick ebfd367 Wednesday commit
pick 30e0ccb Thursday commit
```

`fixup` will squish Tuesday into Monday and remove git history for `Tuesday commit`, like that
commit never happened. If you want to rename Monday in the process, you can edit it like this:

```txt
reword 01d1124 Monday Tuesday commit
fixup 6340aaa Tuesday commit
pick ebfd367 Wednesday commit
pick 30e0ccb Thursday commit
```

This will squish Tuesday's commit into Mondays, and rename it `Monday Tuesday commit`.

### 2.7 Command ```git cherry-pick```

If you need to pull a single commit from another branch, you can `git log` to get that commit's
commit hash, and then switch to the branch you need to pull into and run
`git cherry-pick <commit hash>`.

### 2.8 Force push

If your branch and the upstream (i.e., on Github) branch have diverged, you will be unable to push
your changes. This is common on rebases, or sometimes you don't care about what's upstream because
you know that whatever's on your branch is what needs to be up there. Whatever the reason, you can
do a force push to have the upstream accept your changes by adding a plus to the branch, like so
`git push origin +myBranch`. **Don't do this on a branch multiple people are using**, you will cause
serious git headaches. Also, obviously, this is a good way to lose any upstream changes permanently,
so be careful when using this.

### 2.9 Force pull

If you don't care about what's on your branch, and you just want whatever's on the remote, run
`git fetch --all` (to update your local git so that it knows what's on the remote) and then run
`git reset --hard origin/<branch name>`. **You will lose whatever is on your local branch.**
