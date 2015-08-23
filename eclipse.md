# Eclipse IDE

Eclipse can be setup as an IDE for Haskell. Recently, the maintenance of that IDE has stoped, but it can still be used at own risk. 




## Setup



## Issue on Windows / Eclipse and hslua

Due to bugs in Cabal and maybe ghc, Eclipse's buildwrapper cannot build the `hslua` package on Windows, which disables type-tooltip functionality. The problem seems to be that `hslua` (which is a dependency of `pandoc`) contains C-code, which is not handled well by dynamic cabal. As a workaround, you can install the `hslua-dummy` package, which exports all types and functions of `hslua`, but implements them as `()` and `error`. Since Ampersand doesn't use any `hslua` functionality this will not cause any problems.

Update: I found [an issue](https://github.com/osa1/hslua/issues/22) telling that this is probably caused by using a 32-bit MSys2 but using the 64-bit version of Haskell Platform. 

To install the dummy `hslua` in your ampersand working copy, go to the parent directory of the working copy and clone `hslua-dummy`:

    git clone git@github.com:AmpersandTarski/hslua-dummy.git

Let it use the same sandbox as ampersand:

    cd hslua-dummy
    cabal sandbox init --sandbox=../ampersand/.cabal-sandbox

And install the dummy package with

    cabal install

This will remove the old `hslua` package and update `pandoc` to use the dummy version.
