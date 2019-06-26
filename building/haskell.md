---
description: >-
  To build your own Ampersand compiler is something to avoid as a user. As a
  developer, however, you may have reasons to do this yourself. For instance to
  verify what happens in older versions.
---

# Building an Ampersand Compiler with Stack

[Stack](https://haskellstack.org/) is a build tool for Haskell projects such as Ampersand. The Ampersand compiler is built by stack, which serves the following purposes:

1. to prevent dependency conflicts inside and between Haskell packages that might otherwise cause errors during the compilation process;
2. to generate ampersand compilers for different platforms without headache;
3. to provide a reproducible and reliable build process to developers with diverse development tools, operating systems, and working environments; 
4. to generate images for docker containers without having to learn about building in docker;
5. to accellerate the build process to increase the release frequency of Ampersand.

## Installation

[Haskell](https://www.haskell.org/) comes as part of [Stack](http://haskellstack.org), the build environment of Haskell.

The [instructions to install Stack](http://haskellstack.org) are pretty clear for the various platforms. Make sure you read the part about the STACK\_ROOT environment variable.

Then, go to the path where you have the file `ampersand.cabal`. `stack install` will build the ampersand compiler. NB: If you want to build the ampersand preprocessor as well, the magic spell is `stack install --flag ampersand:buildAll`

