# action-playground

For testing github actions.

See [.github/workflows](.github/workflows):

* release-please: 
  * need to add a fine-grained PAT with read/write for PRs, read/write for contents, and write for workflows
  * make sure in the repo's settings > actions > general, the checkbox "Allow GitHub Actions to create and approve pull requests" is enabled
  * conclusion: not worth it, this repo is poorly maintained and doesn't support any workflow that deviates from a simple single-branch release process. Ugh.
  * using target-branch: main for all release PRs also doesn't produce the intended behavior. Releases triggered from RC branches skip all commits for some reason
  * tried splitting up strategy: release _candidate_ PR from main, then releases from rc branches _into_ main. Not supported well. Total mess, finnicky.
