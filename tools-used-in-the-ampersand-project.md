---
description: >-
  This page lists the tools that are used and for which purpose they are used.
  This list is intended for reference, so it is full of hyperlinks that can
  point you to the right location.
---

# Tools used in the Ampersand project

## Specific tools used in the Ampersand project

<table>
  <thead>
    <tr>
      <th style="text-align:left">Tool</th>
      <th style="text-align:left">Purpose (the hyperlink navigates to the section in this book)</th>
      <th
      style="text-align:left">Knowledge holder</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><a href="https://hub.docker.com/r/ampersandtarski/ampersand-prototype/">Ampersand image</a>
      </td>
      <td style="text-align:left">a docker-image in which we keep the latest version of the Ampersand compiler
        in executable form. It resides in <a href="https://hub.docker.com/r/ampersandtarski/ampersand/">docker-hub</a>.</td>
      <td
      style="text-align:left">all</td>
    </tr>
    <tr>
      <td style="text-align:left">Ampersand compiler</td>
      <td style="text-align:left">An executable that is used to generate software, documentation, and analyses
        from Ampersand-scripts. It is embedded into the Ampersand image and into
        RAP3. There exist multiple instances, so we cannot hyperlink to it.</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://github.com/AmpersandTarski/Ampersand/">Ampersand repository</a>
      </td>
      <td style="text-align:left">a <a href="gitbook/getting-started-with-gitbook.md">repository</a> in which
        we keep Ampersand source code and manage the issues wrt Ampersand. It resides
        on <a href="https://github.com/AmpersandTarski/Ampersand">GitHub</a>.</td>
      <td
      style="text-align:left">all</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://ci.appveyor.com/project/hanjoosten/ampersand">Appveyor</a>
      </td>
      <td style="text-align:left">a service that generates executable files for Windows automatically, each
        time a new release of Ampersand appears. It <a href="releasing-ampersand-and-workflow-details.md">releases the Ampersand compiler</a> for
        Windows automatically, provided all automated tests have passed</td>
      <td
      style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://hub.docker.com/u/ampersandtarski/">Docker Hub</a>
      </td>
      <td style="text-align:left">a repository in which we keep <a href="installation-of-rap/making-docker-images.md">Ampersand images</a>
      </td>
      <td style="text-align:left"><a href="https://github.com/hidde-jan">Hidde-Jan</a>, <a href="https://github.com/stefjoosten">Stef</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.ou.nl/-/IM0403_Rule-Based-Design">GitBook</a>
      </td>
      <td style="text-align:left">a documentation system in which we maintain the <a href="https://ampersandtarski.gitbook.io/documentation">documentation of Ampersand</a> and
        the <a href="https://ampersandtarski.gitbook.io/the-tools-we-use-for-ampersand/">documentation on how we build and maintain the software</a>.
        We use GitBook to allow collaborative editing in the documentation based
        on Git.</td>
      <td style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>, <a href="https://github.com/stefjoosten">Stef</a>,
        <a
        href="https://github.com/EstherHageraats">Esther</a>, <a href="https://github.com/LloydRutledge">Lloyd</a>, <a href="https://github.com/hidde-jan">Hidde-Jan</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://github.com/AmpersandTarski/">GitHub</a>
      </td>
      <td style="text-align:left">an organisation in which we keep all Ampersand git-repos</td>
      <td style="text-align:left">all</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="http://ampersand.tarski.nl/RAP3/">RAP3</a>
      </td>
      <td style="text-align:left">a <a href="functionality-of-rap3/">web-based application</a> for the public
        at large to use Ampersand. This instance is also used as acceptation environment
        for <a href="http://rap.cs.ou.nl/RAP3">the RAP3 instance that is used for students</a> in
        the course <a href="https://www.ou.nl/-/IM0403_Rule-Based-Design">Rule Based Design</a>.</td>
      <td
      style="text-align:left"><a href="https://github.com/LloydRutledge">Lloyd</a>, <a href="https://github.com/stefjoosten">Stef</a>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="http://rap.cs.ou.nl/RAP3">RAP3</a>
      </td>
      <td style="text-align:left">a <a href="functionality-of-rap3/">web-based application</a> that is used
        as production environment for students in the course <a href="https://www.ou.nl/-/IM0403_Rule-Based-Design">Rule Based Design</a>.</td>
      <td
      style="text-align:left"><a href="https://github.com/EstherHageraats">Esther</a>, <a href="https://github.com/LloydRutledge">Lloyd</a>,
        <a
        href="https://github.com/stefjoosten">Stef</a>
          </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://github.com/AmpersandTarski/RAP/">RAP-repo</a>
      </td>
      <td style="text-align:left">a Github repository in which we keep the <a href="installation-of-rap/">source code of RAP </a>.</td>
      <td
      style="text-align:left"><a href="https://github.com/stefjoosten">Stef</a>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.ou.nl/-/IM0403_Rule-Based-Design">Rule Based Design</a>
      </td>
      <td style="text-align:left">a course at the <a href="https://ou.nl">Open Universiteit</a> in which students
        use Ampersand.</td>
      <td style="text-align:left"><a href="https://github.com/stefjoosten">Stef</a>, <a href="https://github.com/EstherHageraats">Esther</a>,
        <a
        href="https://github.com/LloydRutledge">Lloyd</a>, <a href="https://github.com/rvandewetering">Rogier</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><a href="https://travis-ci.org/AmpersandTarski/Ampersand">Travis</a>
        </p>
        <p>
          <img src=".gitbook/assets/travisci-full-color-1.png" alt/>
        </p>
      </td>
      <td style="text-align:left">a service, which runs automated tests on every commit of the Ampersand
        repository on Github. Only the successfully tested commits on the releases
        branch are released</td>
      <td style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>
      </td>
    </tr>
  </tbody>
</table>## Generic tools used in the Ampersand project

<table>
  <thead>
    <tr>
      <th style="text-align:left">Tool</th>
      <th style="text-align:left">Purpose</th>
      <th style="text-align:left">Knowledge holder</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ACE</td>
      <td style="text-align:left">a web-editor that is used within RAP. It has been integrated in the RAP-application
        code.</td>
      <td style="text-align:left"><a href="https://github.com/Michiel-s">Michiel</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">EditPad</td>
      <td style="text-align:left">a text editor that has long been used in the Ampersand project, but not
        any more. A syntax coloring mechanism for Ampersand still exists. This
        editor has been superseded by VScode, because it is being supported by
        a much larger community.</td>
      <td style="text-align:left"><a href="https://github.com/RieksJ">Rieks</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.docker.com/">Docker</a>
      </td>
      <td style="text-align:left">the platform for technology agnostic, fully automated deployment of services,
        which we use to deploy the Ampersand compiler and applications developed
        in Ampersand.</td>
      <td style="text-align:left"><a href="https://github.com/hidde-jan">Hidde-Jan</a>, <a href="https://github.com/stefjoosten">Stef</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://docs.docker.com/compose/">Docker-compose</a>
      </td>
      <td style="text-align:left">a platform for configuring services in a full-fledged application such
        as RAP.</td>
      <td style="text-align:left"><a href="https://github.com/hidde-jan">Hidde-Jan</a>, <a href="https://github.com/stefjoosten">Stef</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><a href="https://git-scm.com/community">Git</a>
        </p>
        <p>
          <img src=".gitbook/assets/logo-2x-1.png" alt/>
        </p>
      </td>
      <td style="text-align:left">the versioning system in which all source code is kept. It enables us
        to work collaboratively on multiple features in parallel, without interfering
        each other&apos;s work.</td>
      <td style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>, <a href="https://github.com/RieksJ">Rieks</a>,
        <a
        href="https://github.com/Michiel-s">Michiel</a>, <a href="https://github.com/hidde-jan">Hidde-Jan</a>, <a href="https://github.com/Oblosys">Martijn</a>,
          <a
          href="https://github.com/stefjoosten">Stef</a>, <a href="https://github.com/sjcjoosten">Sebastiaan</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.graphviz.org/">Graphviz</a>
      </td>
      <td style="text-align:left">a system for generating diagrams, which is used to generate conceptual
        models and data models as part of the documentation generator.</td>
      <td
      style="text-align:left"><a href="https://github.com/stefjoosten">Stef</a>, <a href="https://github.com/hanjoosten">Han</a>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.haskell.org/">Haskell</a>
      </td>
      <td style="text-align:left">the programming language in which the Ampersand compiler is built and
        maintained.</td>
      <td style="text-align:left"><a href="https://github.com/stefjoosten">Stef</a>, <a href="https://github.com/sjcjoosten">Sebastiaan</a>,
        <a
        href="https://github.com/hanjoosten">Han</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.json.org/">JSON</a>
      </td>
      <td style="text-align:left">a simple, standardized, format for communicating data structures. It is
        used to communicate data from the Ampersand-compiler to the generated application.</td>
      <td
      style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>, <a href="https://github.com/Michiel-s">Michiel</a>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://kubernetes.io/">Kubernetes</a>
      </td>
      <td style="text-align:left">a platform for configuring and managing deployed services (such as RAP)
        in an operational environment. Kubernetes is not being used yet in production
        instances of Ampersand.</td>
      <td style="text-align:left"><a href="https://github.com/stefjoosten">Stef</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">LaTeX</td>
      <td style="text-align:left">a typesetting system, which we use to generate PDF&apos;s with. At the
        moment MarkDown is the preferred markup language, so LaTeX&apos;s role
        in the Ampersand project is decreasing.</td>
      <td style="text-align:left"><a href="https://github.com/stefjoosten">Stef</a>, <a href="https://github.com/hanjoosten">Han</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://mariadb.org/">MariaDB</a>
      </td>
      <td style="text-align:left">the database that is used by Ampersand for persistency. This used to be
        MySQL, until MariaDB took over in the Open Source community.</td>
      <td style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>, <a href="https://github.com/Michiel-s">Michiel</a>,
        <a
        href="https://github.com/stefjoosten">Stef</a>, <a href="https://github.com/sjcjoosten">Sebastiaan</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.markdownguide.org/">Markdown</a>
      </td>
      <td style="text-align:left">the language in which Ampersand documentation is written. We use it for
        maximal portability of text over different platforms.</td>
      <td style="text-align:left">all</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://nodejs.org/">Node.js</a>
      </td>
      <td style="text-align:left">the JavaScript framework in which an Ampersand Prototype is generated</td>
      <td
      style="text-align:left"><a href="https://github.com/Michiel-s">Michiel</a>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.npmjs.com/">npm</a>
      </td>
      <td style="text-align:left">the package manager for JavaScript, which guarantees consistency of module
        dependencies in the JavaScript world.</td>
      <td style="text-align:left"><a href="https://github.com/Michiel-s">Michiel</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://pandoc.org/">Pandoc</a>
      </td>
      <td style="text-align:left">a system for document translation and markup, which we use to create a
        host of different document formats</td>
      <td style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://www.haskellstack.org/">Stack</a>
      </td>
      <td style="text-align:left">a build automation environment for Haskell that we use to build the Ampersand
        compiler with. It guarantees consistency of module dependencies within
        the Haskell world.</td>
      <td style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>, <a href="https://github.com/stefjoosten">Stef</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://code.visualstudio.com/">VS-code</a>
      </td>
      <td style="text-align:left">an editor for development of the Ampersand compiler and Ampersand-projects.
        A VScode extension for Ampersand exists that offers syntax coloring.</td>
      <td
      style="text-align:left"><a href="https://github.com/hanjoosten">Han</a>, <a href="https://github.com/RieksJ">Rieks</a>
        </td>
    </tr>
  </tbody>
</table>



