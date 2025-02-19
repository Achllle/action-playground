# action-playground

For testing github actions

See [.github/workflows](.github/workflows):

* release-please: 
  * need to add a fine-grained PAT with read/write for PRs, read/write for contents, and write for workflows
  * make sure in the repo's settings > actions > general, the checkbox "Allow GitHub Actions to create and approve pull requests" is enabled

## behavior of release-please with rc branches

* What happens when a release-please PR is merged on an `rc` (release candidate) branch? When you then make another release from a different `rc` branch, does it properly include the release from the last merge? Is the changelog updated correctly, including on main?
* force pushes work as expected

