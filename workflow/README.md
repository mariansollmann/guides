# Workflow

## Issues
- Mention someone for feedback if needed
- Link to related issues, dependencies or meta-issue

## Pull Requests
- Keep as simple as possible
- Split into isolable sub parts
- Document dependencies between PRs

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
- Is it tested?
- Is it performant?
- Is it maintainable and extensible?
- The owner and the reviewer(s) are responsible for the change and understand its consequences.

## App Release
- Merge clean, isolable states
- Master is always deployable
- Check the latest CI test results at http://ci.cargomedia.ch:8080/
- Changes should be deployed quickly
- Changes since last release: Grep commits in the application as well as in CM with `git log --grep="Merge pull request" {commit SHA}..`
- Change-owners should be available during release
- Monitor infrastructure performance, application performance and logs
