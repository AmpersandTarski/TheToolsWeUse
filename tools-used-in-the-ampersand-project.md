---
description: This page lists the tools that are used and the purpose for which.
---

# Tools used in the Ampersand project

## Specific tools used in the Ampersand project

| Tool | Purpose \(the hyperlink navigates to the section in this book\) | Knowledge holder |
| :--- | :--- | :--- |
| [Ampersand image](https://hub.docker.com/r/ampersandtarski/ampersand-prototype/) | a docker-image in which we keep the latest version of the Ampersand compiler in executable form. It resides in [docker-hub](https://hub.docker.com/r/ampersandtarski/ampersand/). | all |
| Ampersand compiler | An executable that is used to generate software, documentation, and analyses from Ampersand-scripts. It is embedded into the Ampersand image and into RAP3. It is platform dependent, so we cannot hyperlink to it. |  |
| [Ampersand repository](https://github.com/AmpersandTarski/Ampersand/) | a [repository](gitbook/getting-started-with-gitbook.md) in which we keep Ampersand source code and manage the issues wrt Ampersand. It resides on [GitHub](https://github.com/AmpersandTarski/Ampersand). | all |
| [Appveyor](https://ci.appveyor.com/project/hanjoosten/ampersand) | a service that generates executable files for Windows automatically, each time a new release of Ampersand appears. It [releases the Ampersand compiler](releasing-ampersand-and-workflow-details.md) for Windows automatically, provided all automated tests have passed | [Han](https://github.com/hanjoosten) |
| [Docker Hub](https://hub.docker.com/u/ampersandtarski/) | a repository in which we keep [Ampersand images](installation-of-rap/making-docker-images.md) | [Hidde-Jan](https://github.com/hidde-jan), [Stef](https://github.com/stefjoosten) |
| [GitBook](https://www.ou.nl/-/IM0403_Rule-Based-Design) | a documentation system in which we maintain the [documentation of Ampersand](https://ampersandtarski.gitbook.io/documentation) and the [documentation on how we build and maintain the software](https://ampersandtarski.gitbook.io/the-tools-we-use-for-ampersand/). We use GitBook to allow collaborative editing in the documentation based on Git. | [Han](https://github.com/hanjoosten), [Stef](https://github.com/stefjoosten), [Esther](https://github.com/EstherHageraats), [Lloyd](https://github.com/LloydRutledge), [Hidde-Jan](https://github.com/hidde-jan) |
| [GitHub](https://github.com/AmpersandTarski/) | an organisation in which we keep all Ampersand git-repos | all |
| [RAP3](http://ampersand.tarski.nl/RAP3/) | a [web-based application](functionality-of-rap3/) for the public at large to use Ampersand | [Esther](https://github.com/EstherHageraats), [Lloyd](https://github.com/LloydRutledge), [Stef](https://github.com/stefjoosten) |
| [RAP-repo](https://github.com/AmpersandTarski/RAP/) | a Github repository in which we keep the [source code of RAP ](installation-of-rap/). | [Stef](https://github.com/stefjoosten) |
| [Rule Based Design](https://www.ou.nl/-/IM0403_Rule-Based-Design) | a course at the [Open Universiteit](https://ou.nl) in which students use Ampersand. | [Stef](https://github.com/stefjoosten), [Esther](https://github.com/EstherHageraats), [Lloyd](https://github.com/LloydRutledge), [Rogier](https://github.com/rvandewetering) |
| [Travis](https://travis-ci.org/AmpersandTarski/Ampersand) | a service, which runs automated tests on every commit of the Ampersand repository on Github. Only the successfully tested commits on the releases branch are released | [Han](https://github.com/hanjoosten) |

## Generic tools used in the Ampersand project

| Tool | Purpose | Knowledge holder |
| :--- | :--- | :--- |
| ACE | a web-editor that is used within RAP. It has been integrated in the RAP-application code. | [Michiel](https://github.com/Michiel-s) |
| EditPad | a text editor that has long been used in the Ampersand project, but not any more. A syntax coloring mechanism for Ampersand still exists. This editor has been superseded by VScode, because it is being supported by a much larger community. | [Rieks](https://github.com/RieksJ) |
| [Docker](https://www.docker.com/) | the platform for technology agnostic, fully automated deployment of services, which we use to deploy the  Ampersand compiler and applications developed in Ampersand. | [Hidde-Jan](https://github.com/hidde-jan), [Stef](https://github.com/stefjoosten) |
| [Docker-compose](https://docs.docker.com/compose/) | a platform for configuring services in a full-fledged application such as RAP. | [Hidde-Jan](https://github.com/hidde-jan), [Stef](https://github.com/stefjoosten) |
| [Git](https://git-scm.com/community) | the versioning system in which all source code is kept. It enables us to work collaboratively on multiple features in parallel, without interfering each other's work. | [Han](https://github.com/hanjoosten), [Rieks](https://github.com/RieksJ), [Michiel](https://github.com/Michiel-s), [Hidde-Jan](https://github.com/hidde-jan), [Martijn](https://github.com/Oblosys), [Stef](https://github.com/stefjoosten), [Sebastiaan](https://github.com/sjcjoosten) |
| [Graphviz](https://www.graphviz.org/) | a system for generating diagrams, which is used to generate conceptual models and data models as part of the documentation generator. | [Stef](https://github.com/stefjoosten), [Han](https://github.com/hanjoosten) |
| [Haskell](https://www.haskell.org/) | the programming language in which the Ampersand compiler is built and maintained. | [Stef](https://github.com/stefjoosten), [Sebastiaan](https://github.com/sjcjoosten), [Han](https://github.com/hanjoosten) |
| [JSON](https://www.json.org/) | a simple, standardized, format for communicating data structures. It is used to communicate data from the Ampersand-compiler to the generated application. | [Han](https://github.com/hanjoosten), [Michiel](https://github.com/Michiel-s) |
| [Kubernetes](https://kubernetes.io/) | a platform for configuring and managing deployed services \(such as RAP\) in an operational environment. | [Stef](https://github.com/stefjoosten) |
| [MariaDB](https://mariadb.org/) | the database that is used by Ampersand for persistency | [Han](https://github.com/hanjoosten), [Michiel](https://github.com/Michiel-s), [Stef](https://github.com/stefjoosten), [Sebastiaan](https://github.com/sjcjoosten) |
| [Markdown](https://www.markdownguide.org/) | the language in which Ampersand documentation is written | all |
| [Node.js](https://nodejs.org/) | the JavaScript framework in which an Ampersand Prototype is generated | [Michiel](https://github.com/Michiel-s) |
| [npm](https://www.npmjs.com/) | the package manager for JavaScript, which guarantees consistency of module dependencies in the JavaScript world. | [Michiel](https://github.com/Michiel-s) |
| [Pandoc](https://pandoc.org/) | a system for document translation and markup, which we use to create a host of different document formats | [Han](https://github.com/hanjoosten) |
| [Stack](https://www.haskellstack.org/) | a build automation environment for Haskell that we use to build the Ampersand compiler with. It guarantees consistency of module dependencies within the Haskell world. | [Han](https://github.com/hanjoosten), [Stef](https://github.com/stefjoosten) |
| [VS-code](https://code.visualstudio.com/) | an editor for development of the Ampersand compiler and Ampersand-projects. A VScode extension for Ampersand exists that offers syntax coloring. | [Han](https://github.com/hanjoosten), [Rieks](https://github.com/RieksJ) |





