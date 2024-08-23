# Git Utilities

This repository collects some utilities which are required on a frequent basis
but too complex for a Bash one-liner.

## follow-remote-merge
### Installation

Either `sudo install follow-remote-merge /usr/local/bin` or `install follow-remote-merge ~/.local/bin`.

### Usage

```
./follow-remote-merge: [OPTION]... [target-branch]

Follow a merge that was performed on a remote platform, e.g. GitHub or GitLab.
If HEAD is contained in the target branch, HEAD is switched to the target
branch and the source branch is deleted.

The target branch defaults to `develop`, `main`, or `master`, in that
order.

OPTIONS:

  -C DIRECTORY Execute git commands in DIRECTORY. Defaults to PWD.
  -f, --force  Skip checks when moving to target branch.
  -h, --help   Print this message and exit.

Examples:
follow-remote-merge
follow-remote-merge develop
follow-remote-merge -C ~/repos/some-repo -f weird-default-branch
```

## migrate-from
### Installation

Either `sudo install migrate-from /usr/local/bin` or `install migrate-from ~/.local/bin`.

### Usage

```
./migrate-from: [OPTION]... REMOTE_URI [SRC_BRANCH]

Set the currently active local branch to SRC_BRANCH from the repository at
REMOTE_URI. The history of the local branch is lost and replaced with the
history of SRC_BRANCH.

IF SRC_BRANCH is not given, the default branch of the remote repository is used.

The REMOTE_URI is the URI of the remote repository. It can be a URL or a path to
a local repository. It will be added to the current repository as a remote
repository with a random name but removed after the operation.


OPTIONS:

  -C DIRECTORY Execute git commands in DIRECTORY. Defaults to PWD.
  -h, --help   Print this message and exit.

Examples:
migrate-from "/path/to/repo"
migrate-from "/path/to/repo" develop
migrate-from "git@github.com:MaxG87/git-utils.git"
```
