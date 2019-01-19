# branch-gc

I kept accumulating branches either pushed to github or in my local dev
environments that were stale, they'd already been merged upstream, but
accumulated over time. I wrote this script as a utility to tidy up, hope


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
