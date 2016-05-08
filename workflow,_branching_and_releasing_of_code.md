# Workflow, branching and releasing of code

Working with Git gives a lot of possibilities on how to work as a team. I have been looking around what other teams do. For us, I guess we should keep it simple, and use the good stuff invented elsewhere. I think we should adapt to [gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow), witch uses [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow). 

The core idea of [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) is that each change is triggered by its own issue. So for each issue, a specific branch is created. It is developed, and once the developer(s) think it is ready, they do a pull request. Then, other collaborators inspect the code, do some testing. Once there is agreement that the fix/enhancement is good enough, then it can be pulled into the master. 

In [gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) we have the same thing, but there is also a develop branch. 

## Release notes

Every time someone pulls a feature branch into the development branch, the release notes should be updated with a small description of the change. If we all keep up to this habit, it will become pretty easy to do a release, including an appropriate set of release notes. 

