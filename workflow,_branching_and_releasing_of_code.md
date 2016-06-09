# Workflow, branching and releasing of code

Working with Git gives a lot of possibilities on how to work as a team. I have been looking around what other teams do. For us, I guess we should keep it simple, and use the good stuff invented elsewhere. I think we should adapt to [gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow), witch uses [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow). 

The core idea of [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) is that each change is triggered by its own issue. So for each issue, a specific branch is created. It is developed, and once the developer(s) think it is ready, they do a pull request. Then, other collaborators inspect the code, do some testing. Once there is agreement that the fix/enhancement is good enough, then it can be pulled into the master. 

In [gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) we have the same thing, but there is also a develop branch. 

## Release notes

Every time someone pulls a feature branch into the [development branch](https://github.com/AmpersandTarski/Ampersand/tree/development), the release notes should be updated with a small description of the change. If we all keep up to this habit, it will become pretty easy to do a release, including an appropriate set of [release notes](https://github.com/AmpersandTarski/Ampersand/blob/development/ReleaseNotes.md). 

## Releasing at Github
Recently we have decided to release regularly. This means, once every 4 weeks. Of course, we want this to be as smooth as can be. Ideally, we want it fully automated. 



## Pre-release steps

* In `development` branch:
  * `ampersand.cabal`: 
    * bump the version number to release
  * `ReleaseNotes.md` : 
    * rename the "unreleased changes" section to the new version
    * add new "unreleased changes" section
  * `stack.yaml` : 
    * bump to use latest LTS version, and check whether extra-deps still needed
* create pull request to master
* Ensure travis-ci builds succesfully
* merge pull request into master
* [Draft a new release](https://github.com/AmpersandTarski/Ampersand/releases/)
  * Set title e.g. `release v3.5.1 (17 may 2016)`
  * Set tag e.g. `v3.5.1`
* build windows executable and add it to the release  
