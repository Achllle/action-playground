# action-playground

For testing github actions.

See [.github/workflows](.github/workflows):

* release-please:
  * need to add a fine-grained PAT with read/write for PRs, read/write for contents, and write for workflows
  * make sure in the repo's settings > actions > general, the checkbox "Allow GitHub Actions to create and approve pull requests" is enabled
  * conclusion: not worth it, this repo is poorly maintained and doesn't support any workflow that deviates from a simple single-branch release process. Ugh.
  * using target-branch: main for all release PRs also doesn't produce the intended behavior. Releases triggered from RC branches skip all commits for some reason
  * tried splitting up strategy: release _candidate_ PR from main, then releases from rc branches _into_ main. Not supported well. Total mess, finnicky.
  * trying to just run release-please on rc branches with target to main. Doesn't work like that because the action doesn't run again when the PR is created since it doesn't run on main...
  * trying to run with two separate actions again on main, but this time not to create release candidate but instead to just create the release tag and release. Failed, it considered a breaking change on main that didn't exist in the rc branch for the release: #18
  * trying to separate branches again.
  * trying to set target branch unset - didn't work either
  * final try: manifest file hacking - with fully isolated releases in rc branches. Fully give up, it's just too finnicky. When I had created a manual release and tag it didn't recognize that and somehow tried to release under the existing release which ofcourse failed.

* SemVer action (ietf-tools/semver-action):
  * need to give write permissions for writing tags
  * works with versions such as v1.2.3-alpha1
  * caution: pushing a tag inside the workflow this server-action is in will not trigger a different workflow that has the `on: push: tags` event trigger (github policy to avoid accidental recursion). Either use a different PAT for the triggering workflow or better, use a `workflow_run` trigger with a check to see if the workflow run was successful.
