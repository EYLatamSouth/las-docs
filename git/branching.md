<!-- omit in toc -->
# Branching

Create new feature branches off of `master` by running `git checkout -b <name>`. See below for
naming conventions.


- [1. Naming branches](#1-naming-branches)
- [2. Cleaning up](#2-cleaning-up)


## 1. Naming branches

Branches have the following naming convention:

```txt
<username>/<ticket-number>-<branch-name>
```

- Username: Does not have to be your github handle, but should be easily identifiable as you. Be
  consistent and use one for all of your branches (at least on the same project).
- Ticket number: The ticket number that your work is tied to, whether it's the JIRA ticket (xyz-123)
  or just the Github issue number (123)
- Branch name: The name of your branch, briefly describing the work (i.e., user-routes)

Branches should be all lowercase with dashes separating all words.

## 2. Cleaning up

Delete your branches after they're merged.

**Examples**

Assuming a dev's username is jsmith

A branch for adding user routes, related to Github ticket #35

`jsmith/35-add-user-routes`

A branch for updating the Organization contract, related to JIRA ticket XYZ-235

`jsmith/xyz-235-update-organization`
