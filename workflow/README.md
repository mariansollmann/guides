# Workflow

We're using GitHub as a repository server and issue tracker.

## Repository setup
We're using a pull-request workflow where every developer has his own clone ("fork") of the original repository ("upstream").
To propose a patch, the developer submits a pull-request from his *feature-branch* to the upstream repository.

For this workflow to work properly, make sure to have two git remotes on your local repository clones:
- *origin*: Your remote clone on github (e.g. `git@github.com:<username>/guides.git`)
- *upstream*: The upstream clone on github (e.g. `git@github.com:cargomedia/guides.git`)

If you initially clone from your github remote, the *origin* will already be set. To add the *upstream* remote, run something like:
```
git remote add upstream git@github.com:cargomedia/guides.git
```

## Pull Requests
- Keep as simple as possible
- Split into isolable sub parts
- Document dependencies between PRs

### git/hub workflow

1. Update your *upstream* remote, create a new branch off of `upstream/master` and push it to your *origin*:
```
git fetch upstream
git checkout --no-track -b my-feature upstream/master
git push --set-upstream origin my-feature
```
With cargomedia's mac deployment the above is available as a git alias:
```
git branch-feature my-feature
```
If resolving an issue it is recommended to name your branch `issue-<issue-number>`:
```
git branch-feature issue-123
```

2. Work as usual, then push and create a pull-request
```
git commit
git push
hub pull-request
```

### [github-issues](https://github.com/cargomedia/github-issues) workflow

1. Open an issue, and create a corresponding branch off of `upstream/master`
```
gi open 'Issue title'
```

2. Work as usual, then push and create a pull-request
```
git commit
gi push
gi pull-request
```

## Commits
- Commit often
- Commit working states when possible (build should be green)
- Explain briefly *what* and *why* if necessary. [Add summary if your message is longer.](http://stackoverflow.com/questions/4126442/git-commit-format)

Further reading: http://dev.solita.fi/2013/07/04/whats-in-a-good-commit.html

## Reviewing
- Owner: Mention for review
- Owner: Mention for merge
- Merge upstream before asking for review
- Merge commits: Check conflicts!
- Is it tested? Is it performant? Is it maintainable and extensible?
- The owner and the reviewer(s) are responsible for the change and understand its consequences.

## App Release
- Merge clean, isolable states
- Master is always deployable
- Changes should be deployed quickly. Some projects use [pulsar](https://github.com/cargomedia/pulsar-conf-cargomedia) for deployments.
- Change-owners should be available during release
- Monitor infrastructure performance, application performance and logs
