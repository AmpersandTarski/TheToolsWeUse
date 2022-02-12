---
description: >-
  Most of us use VS Code as a code editor. This page is about some handy
  configuration tips.
---

# Development using VS Code

## Agreements about the development of code

### Working with feature branches

All changes that are made to the code is done in feature branches. Such a branch should have a specific goal. Normally, this is documented in a single github issue. While the work can take some time, eventually a pull request is made in order to merge it into main. There are several requirements that must be met before a pull request can be merged. &#x20;

### Releasenotes

Every feature must be briefly documented in the releasenotes. A github action is in place that will notify if the releasenotes are not changed.&#x20;

### Code formatting

All code must be formatted in a consistent way. We use [ormolu](https://hackage.haskell.org/package/ormolu), a standard code formatting tool for Haskell. We only accept Haskell files that are properly formatted. This is enforced by a new [github action](https://github.com/mrkkrp/ormolu-action#ormolu-action).&#x20;

In order to use ormolu, you have to make sure it is available. Hopefully, some time in future, this will be installed automatically. Until then, you have to in stall it youself:

```
stack install ormolu
```



{% hint style="info" %}
If you use the devcontainer functionality (available in vscode), your code is auto-formatted by default. In other cases, you need to do that yourself. When merging code into the main branch, it should be formatted correctly. You can autoformat all haskell files with the command:

```bash
stack exec ormolu -- --mode inplace $(git ls-files '*.hs')
```
{% endhint %}

### Devcontainer

We provide a standard developer container to the developers of Ampersand. Documentation about this awsome VScode feature can be found [here](https://code.visualstudio.com/docs/remote/containers).

