# Haskell

## Installation
On a windows machine, installing Haskell should be pretty straitforeward:

At the time of writing, I am installing using [MinGHC](https://www.haskell.org/downloads/windows) (The Haskell Platform might work too, but if you want to use Atom  as an IDE, you need MinGHC).

  1. Download [MinGHC installer for GHC 7.10.2 \(64-bit\)](https://github.com/fpco/minghc/releases/download/2015-08-13/minghc-7.10.2-x86_64.exe)
  2. Run the installer
  3. Go to your ampersand location:
     * cd <path of where you have ```ampersand.cabal    ```
  4. cabal update
  5. cabal sandbox init
  6. cabal install
  
For some reason, the `cabal install` command seems to choke over packages randomly. In such a case, you will see:

```
cabal: Error: some packages failed to install:
   ...<list of packages>... 
```
That's annoying, but no sweat, just try again:
  * cabal install

Oops: This does not work. I eventually get the following error:
```
Linking dist/dist-sandbox-1983fae3\build\ampersand\ampersand.exe ...
ghc.exe: could not execute: C:\Users\hjo20125\AppData\Local\Programs\minghc-7.10
.2-x86_64\ghc-7.10.2\lib/../mingw/bin/gcc.exe
cabal: Error: some packages failed to install:
ampersand-3.2.0 failed during the building phase. The exception was:
ExitFailure 1
```

Some looking around, I see that I have two versions of gcc on my system. Both of mingw, but from different versions. However, the one added to my system is the one up front in the path. Note that this only happens at link-time. ghc itself already built everything.

Now what to do?? (I created an issue)

