# Haskell

## Installation of Haskell

[Haskell](https://www.haskell.org/) comes as part of [Stack](http://haskellstack.org), the build environment of Haskell.

The [instructions to install Stack](http://haskellstack.org) are pretty clear. Make sure you read the part about the STACK\_ROOT environment variable.

Then, go to the path where you have the file `ampersand.cabal`. `stack install` will build the ampersand compiler. NB: If you want to build the ampersand preprocessor as well, the magic spell is `stack install --flag ampersand:buildAll`

