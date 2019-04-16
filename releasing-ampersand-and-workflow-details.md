---
description: >-
  This page is a work instruction for whoever does the periodic release. For now
  we have a semi-automated procedure, because the CI/CD process is not yet fully
  automated as well.
---

# How to release an Ampersand upgrade

Working with Git gives many possibilities on how to work as a team. I have been looking around what other teams do. For us, I guess we should keep it simple, and use the good stuff invented elsewhere. I think we should adapt to [gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow), which uses [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow).

The core idea of [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) is that each change is triggered by its own issue. So for each issue, a specific branch is created. It is developed, and once the developer\(s\) think it is ready, they do a pull request. Then, other collaborators inspect the code, do some testing. Once there is agreement that the fix/enhancement is good enough, then it can be pulled into the master.

In [gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) we have the same thing, but there is also a development branch.

## Release notes

Every time someone pulls a feature branch into the [development branch](https://github.com/AmpersandTarski/Ampersand/tree/development), the release notes should be updated with a small description of the change. If we all stick to this habit, it will become pretty easy to do a release, including an appropriate set of [release notes](https://github.com/AmpersandTarski/Ampersand/blob/development/ReleaseNotes.md).

## Releasing at Github

We release Ampersand every four weeks. Of course, we want this to happen as smoothly as can be. Ideally, we want it fully automated. Yet, some manual tasks are required. This is described in the following paragraph.

## Pre-release steps \(what to do\)

1. In `development` branch, modify the following files[1](releasing-ampersand-and-workflow-details.md#myfootnote1):
   * `package.yaml (and ampersand.cabal)`: 
     * Change the version number to the next release number.
   * `ReleaseNotes.md` : 
     * Rename the "unreleased changes" section to the new version
     * Add a new "unreleased changes" section for the next release.
2. Push your modifications to GitHub. This will trigger automated testing by Travis.
3. Ensure that travis-ci builds succesfully:
   * check the [build at travis](https://travis-ci.org/AmpersandTarski/Ampersand)
4. Create a pull request to the

   [master from the compare with development](https://github.com/AmpersandTarski/Ampersand/compare/master...development)

   :

   [2](releasing-ampersand-and-workflow-details.md#myfootnote2)

   ![](.gitbook/assets/comparing-master-and-development.PNG)

   ![](.gitbook/assets/create-pull-request.PNG)

   Press the green button to create the pull request. We create a pull request so the release leaves a proper administrative trail in GitHub.

5. Wait in [Travis](https://travis-ci.org/AmpersandTarski/Ampersand) for all tests to complete, and then pull the pull-request into the [master](https://github.com/AmpersandTarski/Ampersand/)[3](releasing-ampersand-and-workflow-details.md#myfootnote3).
6. Unfortunatly, currently Appveyor does not build properly. This will be fixed when cabal version 3.0 wil be used. Therefor, both executables have to be build manually on a windows machine and added to the released artefacts. For the time being, the next steps are not working:
7. ~~Now that the master branch contains the new functionality, it will take some time for Appveyor to build the windows executable.~~
8. ~~Wait until~~ [~~appveyor is ready crafting the release~~](https://ci.appveyor.com/project/hanjoosten/ampersand)~~. This should take about 15 minutes.~~
9. Modify the title of the [newly created release](https://github.com/AmpersandTarski/Ampersand/releases/latest).
   * press the edit button, and add the current date to the title. 
   * Also add the following line into the description field:

     ```text
     [Release notes](https://github.com/AmpersandTarski/Ampersand/blob/master/ReleaseNotes.md)
     ```

![](.gitbook/assets/modify-release-title.PNG)

1. Currently, the windows executables are not deployed by appveyor. This is to be fixed. Until then, you can generate them for yourself on a windows machine. use \` stack install --flag ampersand:buildAll\` to generate them and add them to the release.

Notes, tips and tricks:

[1](releasing-ampersand-and-workflow-details.md): Looking for `ampersand.cabal` and `ReleaseNotes.md`? Want to know where they are located? Look in Github for the commit of the previous release. It shows changes were made to these files. From there, open their current \(!\) version. Please make sure your Git is working in the development branch. [2](releasing-ampersand-and-workflow-details.md): This and most of the following actions are done from within the ampersand repository at github. [3](releasing-ampersand-and-workflow-details.md): At the bottom of the page in GitHub, you will find the buttons to merge this release. Please drop a note to describe new features.

