---
description: >-
  This list gives an exhaustive overview of tools and technologies
  used in the Ampersand project. It explains the purpose for using it and the
  project member(s) who know about it.
---

# Introduction

In the early days of the development of Ampersand, it was a single person's project. Haskell was used as programming language, and the source code was kept on a single PC. Fortunately, things have evolved. Now we have a team, and we use quite a lot of open source tooling to help us along. The downside is that not everybody in the team knows all there is to know about the tooling. The purpose of this guide is to help out. It will also be a great place to start for new team members. Another purpose of this book is to get used to the [GitBook](https://www.gitbook.com), that is used to write this documentation.

The [up to date version of this book](http://ampersandtarski.gitbooks.io/the-tools-we-use-for-ampersand/) is published automatically every time a commit is done to the master branch.

# Specific tools used in the Ampersand project

| Tool | Purpose | Knowledge holder |
| :--- | :--- | :--- |
| [Ampersand](https://github.com/AmpersandTarski/Ampersand/) | a repository in which we keep Ampersand source code | [Rieks](https://github.com/RieksJ), [Stef](https://github.com/stefjoosten), [Michiel](https://github.com/Michiel-s), [Esther](https://github.com/EstherHageraats) |
| [Appveyor](https://ci.appveyor.com/project/hanjoosten/ampersand) | a service that releases the Ampersand compiler automatically, provided all automated tests have passed | [Han](https://github.com/hanjoosten) |
| [Docker Hub](https://hub.docker.com/u/ampersandtarski/) | a repository in which we keep Ampersand images | [Hidde-Jan](https://github.com/hidde-jan), [Stef](https://github.com/stefjoosten) |
| [GitBook](https://www.ou.nl/-/IM0403_Rule-Based-Design) | a repository in which we keep Ampersand Documentation | [Han](https://github.com/hanjoosten), [Stef](https://github.com/stefjoosten), [Esther](https://github.com/EstherHageraats), [Lloyd](https://github.com/LloydRutledge), [Hidde-Jan](https://github.com/hidde-jan) |
| [GitHub](https://github.com/AmpersandTarski/) | a project in which we keep all Ampersand git-repos | all |
| RAP | a web-based application for the public at large to use Ampersand | [Stef](https://github.com/stefjoosten), [Han](https://github.com/hanjoosten), [Michiel](https://github.com/Michiel-s) |
| [Rule Based Design](https://www.ou.nl/-/IM0403_Rule-Based-Design) | an Ampersand Course | [Stef](https://github.com/stefjoosten), [Esther](https://github.com/EstherHageraats), [Lloyd](https://github.com/LloydRutledge), [Rogier](https://github.com/rvandewetering) |
| Travis | a service, which runs automated tests on every commit of the Ampersand repository on Github \(the origin\). | [Han](https://github.com/hanjoosten) |

# Generic tools used in the Ampersand project

| Tool | Purpose | Knowledge holder |
| :--- | :--- | :--- |
| [Docker](https://www.docker.com/) | the platform for technology agnostic, fully automated deployment of Ampersand and applications developed in Ampersand. | [Hidde-Jan](https://github.com/hidde-jan), [Stef](https://github.com/stefjoosten) |
| [git](https://git-scm.com/community) | the versioning system in which all source code is kept | [Han](https://github.com/hanjoosten), [Rieks](https://github.com/RieksJ), [Michiel](https://github.com/Michiel-s), [Hidde-Jan](https://github.com/hidde-jan), [Martijn](https://github.com/Oblosys), [Stef](https://github.com/stefjoosten), [Sebastiaan](https://github.com/sjcjoosten) |
| [Graphviz](https://www.graphviz.org/) | a system for generating diagrams, which is used to generate conceptual models and data models as part of the documentation generator. | [Stef](https://github.com/stefjoosten), [Han](https://github.com/hanjoosten) |
| [Haskell](https://www.haskell.org/) | the programming language in which the Ampersand compiler is built | [Stef](https://github.com/stefjoosten), [Sebastiaan](https://github.com/sjcjoosten), [Han](https://github.com/hanjoosten) |
| [JSON](https://www.json.org/) | a simple, standardized, format for communicating data structures. It is used to communicate data from the Ampersand-compiler to the generated application. |  |
| [MariaDB](https://mariadb.org/) | the database that is used by Ampersand for persistency | [Han](https://github.com/hanjoosten), [Michiel](https://github.com/Michiel-s), [Stef](https://github.com/stefjoosten), [Sebastiaan](https://github.com/sjcjoosten) |
| [Markdown](https://www.markdownguide.org/) | the language in which Ampersand documentation is written | all |
| [Node.js](https://nodejs.org/) | the language in which an Ampersand Prototype is generated | [Michiel](https://github.com/Michiel-s) |
| [npm](https://www.npmjs.com/) | the package manager for JavaScript, which guarantees consistency of module dependencies in the JavaScript world. | [Michiel](https://github.com/Michiel-s) |
| [Pandoc](https://pandoc.org/) | a system for document translation and markup, which we use to create a host of different document formats | [Han](https://github.com/hanjoosten) |
| [Stack](https://www.haskellstack.org/) | the installation environment for Haskell, which guarantees consistency of module dependencies within the Haskell world. | [Han](https://github.com/hanjoosten), [Martijn](https://github.com/Oblosys) |
| [VS-code](https://code.visualstudio.com/) | an editor for development of Ampersand and Ampersand-projects | [Han](https://github.com/hanjoosten), [Rieks](https://github.com/RieksJ) |


## Contributions to the documentation

If you have anything to fix or details to add, just post a comment next to the paragraph. We really appreciate if you do so, because our readers know best what it is they are looking for in the docs.

You can do that by clicking the '+' icon that appears when you hover above the paragraph. Don't be shy! Try it out!

## Licence

Unless otherwise specified, everything in this repository is covered by the following licence:

![Creative Commons Attribution-ShareAlike 4.0 International](https://licensebuttons.net/l/by-sa/4.0/88x31.png)

_**Ampersand Documentation**_ by the [the Ampersand team](http://www.gitbook.com/@ampersandtarski/) is licensed under a [Creative Commons Attribution 4.0 International Licence](http://creativecommons.org/licenses/by-sa/4.0/).

Based on a work at [https://github.com/AmpersandTarski/TheToolsWeUse](https://github.com/AmpersandTarski/TheToolsWeUse)

