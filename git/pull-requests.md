<!-- omit in toc -->
# Pull Requests

When you have work that is ready to be reviewed, create a pull request (PR) on the repository.

- [1. Creating a Pull Request](#1-creating-a-pull-request)
  - [1.2 Creating the PR](#12-creating-the-pr)
  - [1.3 Reviewing the PR](#13-reviewing-the-pr)
  - [1.4 Responding to reviews](#14-responding-to-reviews)
  - [1.5 Why we want you to do this](#15-why-we-want-you-to-do-this)
- [2. Labels](#2-labels)

## 1. Creating a Pull Request

### 1.2 Creating the PR

1. Open PR with title `<description of PR> (ticketNumber)`.
   1. e.g., `Created new partner form component (DIC-234)`
   2. If it's a work in progress, prefix title with `WIP:`
2. Add a description to your PR. If there is a
   [Github PR template](https://help.github.com/articles/about-issue-and-pull-request-templates/),
   follow it, otherwise summarize your PR's changes and detail how people can check your work.
3. Add labels ([see below for details](#Labels)).
4. Add developers as reviewers.
5. Add any product/QA people as assignees as necessary.

### 1.3 Reviewing the PR

Code reviews are important, as they spread knowledge of the codebase to more developers, and provide
excellent learning opportunities for reviewers and reviewees.

As a rule of thumb, PRs need two approvals to be merged.

1. Review the code, add comments and either `approve` or `request changes`.
2. If you approve:
   1. If you are the first person to approve, then you don't need to do anything else.
   2. If you are the second person to approve, then you can merge and delete the pull request.
   3. If you are the second person to approve, but you're not confident in your approval (for
      example, you want to wait for the tech lead to approve), then it's okay to keep the
      `Status: Ready for Review` tag.
3. If you're requesting changes:
   1. Remove the `Status: Ready for Review` label and add `Status: Revisions Needed`

### 1.4 Responding to reviews

When you receive comments on your PRs, you can either make the requested changes or argue for why
the changes shouldn't be made. When either of these occur, resolve the conversations on Github.

When you've resolved the conversations, change the label back to `Status: Ready for Review` and
click the Re-request review link next to there name in the pull request's merge box.

### 1.5 Why we want you to do this

It's crucial to productivity on large development teams working in multiple repos. PRs can go
through days or weeks of the review process or sitting idle in some cases. When you assign people
correctly and use the right labels, it increases the visibility of those PRs and devs are also able
to see every actionable PR associated with them at a glance.

Labeling also makes it easier to take action based on date/priority/status/etc. I.e. let's get all
`Type: Bug` tickets merged in ASAP, or `Priority: Critical` tickets, etc.

## 2. Labels

Attach labels to your PR. There should be 3 labels on each PR, `Type`, `Status`, and `Priority`
(except for WIPs, which you leave without labels until ready for review).

- Type label
  - Enhancement: Addition of a feature
  - Bug: Bugfix
  - Maintenance: Cleanups, refactors, linting, docs, etc
- Status label
  - Blocked/On Hold: Cannot be merged for misc reasons
  - Ready for Review
  - Revisions Needed
- Priority: Priority is assumed to be medium unless otherwise stated.
  - Critical
  - Low


If you cloned your repo using an ssh key, then you'll need to generate a
[Personal Access Token](https://github.com/settings/tokens) and it will prompt you for that instead
of your password (and then it will ask you to make a password). This is different from your ssh key.
