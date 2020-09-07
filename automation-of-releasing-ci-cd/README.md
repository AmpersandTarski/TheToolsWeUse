---
description: This page describes the release train for Ampersand.
---

# Automation of releasing \(CI/CD\)

### The purpose of automation.

The release of Ampersand is largely automated because we want:

1. to save ourselves work;
2. to release frequently in a predictable rythm, to bring new functionality to users quickly and predictably;
3. reliable releases, to prevent our mistakes to hit users and to avoid delays caused by the release process;
4. reproducible releases, to allow any team members to step in when the release is due.

### What we want to achieve.

#### Version managment

![](../.gitbook/assets/logo-2x-1.png)

First of all, we want to be **in control** of our software. We use Git\(hub\) to do version management.  We use git flow strategy. We have a master branch that holds the code of the latest stable release. Then we have a development branch that holds the latest added features and bugfixes. We want this branch to be stable too. It must be buildable at all times, and no half-on-its-way functionality should be in it. For new features or other issues, we use feature branches. These branches are work in progress. They might be buildable, or they might not. Feature branches should be used for work in progress only. This keeps the amount of branches manageable. Tags can be created for all kind of other reference purposes to specific commits.

{% hint style="info" %}
To learn more about Git, head over to [this documentation](https://git-scm.com/).
{% endhint %}

#### Automatic build

![](../.gitbook/assets/travisci-full-color-1.png)

Each time a modification of the code is committed to our Github repository, we want to provide answers to a couple of questions: 

1. Can the modified software be built?
2. If so, can we be confident that it doesn't break earlier working features?

To answer these questions, we use Travis-ci to build and do a regression test. This is triggered **whenever a new commit is done** on any branch in the Ampersand repo. 

{% hint style="info" %}
Configuration of what should happen when a commit is done is specified in the _**.travis.yml**_ file in the root directory of the repo. 
{% endhint %}

In brief, the following actions take place

1. Build the application \(using stack\);
2. Run the quickcheck tests \(currently used to verify the parser and prettyprinter\);
3. Run the tests in the regression testset;
4. Depending on if the above was successful, we want to notify specific users and/or systems.
5. If the above was successful, and depending on the branch, a new tag is created at the github repo, as start of a release. Also, built artifacts are being added to the new draft release.

![](../.gitbook/assets/appveyor_logo.svg.png)

We also make use of **Appveyor** to build the application. While travis-ci uses linux, AppVeyor uses Windows. By using Appveyor as well, we can provide windows executables in the release as well. To be able to add windows binary executables to a release, we have AppVeyor build from the same commit. This is triggered whenever a new tag is attached to a commit in the Ampersand repo.

{% hint style="info" %}
Configuration of what should happen when a commit is done is specified in the _**.appveyor.yml**_ file in the root directory of the repo.
{% endhint %}

In brief, the following actions take place \(see the .appveyor.yml file for details\):

1. Build the application \(using chocolatry and cabal\); 
2. Upon success, Appveyor adds the artifacts it has built to the release from the current tag.



