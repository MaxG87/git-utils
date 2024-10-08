# Git Utilities

This repository collects some utilities which are required on a frequent basis
but too complex for a Bash one-liner.

## Installation

The explanation assumes that all scripts were downloaded already. The most
convenient way to do this is to clone the repository.

Installation of the scripts is done by copying them to a directory in the
`PATH` and to make them executable. For a system-wide installation, `sudo
install <SCRIPT> /usr/local/bin` can be used. For an installation only for the
current user, `install <SCRIPT> ~/.local/bin` is recommended.


## follow-remote-merge

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

## do-on-all-gits

### Usage

```
./do-on-all-gits: [OPTION]... [--] COMMAND

Execute COMMAND in all git repositories found in the working directory.

The first token not matching an option is considered to be start of COMMAND to
run in each repository. If unsure, use '--' to mark the end of options.

Be aware that all kind of shell expansions happen before the command is
executed. In particular, globbing (e.g. '*.png') will match files in the
current directory, not in the git repositories. In order to achieve this, you
need to run the command in a subshell, e.g. 'sh -c "echo *.png"'.


OPTIONS:

  -C DIRECTORY Parent directory of the git repositories. Default is the current
               directory.
  -I STRING    Replace occurrences of STRING in COMMAND with the path to the
               git repository. Default is '%'.
  -P N         Run up to N processes in parallel. Default is 0, meaning run as
               many processes as possible.
  -h, --help   Print this message and exit.
  --           End of options. The COMMAND must be specified after this.


Examples:
do-on-all-gits -P 4 -I % -- git -C % pull
do-on-all-gits -C ~/repositories -I % -- echo "Repository: %"
```
