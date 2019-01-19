# branch-gc

I kept accumulating branches either pushed to github or in my local dev
environments that were stale, they'd already been merged upstream, but
accumulated over time. I wrote this script as a utility to tidy up, 
hopefully its useful.

The workflow case its targeting is a project repo, with protected master,
and users contributing branches from forks, with squashed commits on the pr.
This seems to cause some confusion for alot of git tools on whether the
branch is merged since the branch commits are not on the mainline. This utility
instead queries github apis to determine if a pull request existed that
merged the branch.


# Install

Its in python (probably worth a rewrite in go). The only challenging
dependency is pygit2 which needs a recent version of libgit2. On osx
brew can handle that for. Linux environments a recent distro or a source
compile are needed.

```
$ virtualenv branch-gc
$ source branch-gc/bin/activate
$ pip install -r requirements.txt
```


# Cli

```
Usage: branch-gc [OPTIONS] COMMAND [ARGS]...

  Utility Script for tidying up git(hub) branches

  For local branches, it will look for corresponding pull-requests that have
  been merged and then remove the local branch.

  For github branches on a fork, it will query for branches that have been
  merged via pull-request, and then remove them.

Options:
  --help  Show this message and exit.

Commands:
  github  Garbage collect merged github branches
  local   Garbage collect merged local branches
```

Example cleanup github branches in a fork, all commands support dryrun

```
branch-gc github --repo cloud-custodian
```

Example cleanup local branches in a repo by examining prs merged over the last 90 days

```
branch-gc local --repo cloud-custodian --owner cloud-custodian --max-days=90
```
