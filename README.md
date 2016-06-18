# jenkins-tutorial
Jenkins tutorial using git.

## Build Triggers
- `Build when a change is pushed to Github`option is checked.
- Since jenkins is working on localhost, previous option is not worked. Github can't connect our localhost directly. So we used **ngrok** to create tunnel.


Now we are trying to push our repository to Github when we build our repository in Jenkins.
## Post-build Actions
- **Add post-build action** drop box is clicked.
- **Git Publisher** option is selected.
- **Push Only If Build Succeeds** option is selected.
- **Branch to push** option is filled by *master*
- **Target remote name** option is filled by *origin*

## Branches to Build
- **Branch Specifier** is left blank for jenkins to track all branches.

## How to merge branches that successfully build and push to remote master via Jenkins?
- [1] is a good article.

[1]: https://www.cloudbees.com/blog/dont-phunk-my-stable-branch-jenkins-pre-tested-commits-stop-breaking-stable-branches "Pre-tested commits"
