# Publish binaries online

We have a [repository, where we can place pre-built binaries](https://github.com/AmpersandTarski/webFiles/tree/master/executables).

Whoever is using a specific OS (Windows, OS X, ..) could update the version once in a while. This enables users to install Ampersand without the need to build it from scratch. 

## What should be inside the compressed file?

  * The binary itself (duh)
  * A file named VERSION.txt, containing the output of `ampersand --version`

## Windows procedure

Currently, in the installation section of the ampersand user documentation there exists a link to ampersand.zip, as it is in the master branch of 

To create a zip file like that, you need to be on a windows machine. (there is no cross-compiler available as far as I know). 

I use the following batch file to create ampersand.zip:

```.sh
@ECHO off
REM -- Settings, to be set according to the machine where the releas is built. 
set WindowsBuildLocation=D:\data\hjo20125\Git\webFiles\executables\windows\
set AMPERSANDEXE=D:\Data\hjo20125\AppData\Roaming\local\bin\ampersand.exe
set ZIP="D:\Program Files (x86)\Atlassian\SourceTree\tools\7za.exe"

REM --- Replace VERSION.txt
del %WindowsBuildLocation%\VERSION.txt
%AMPERSANDEXE% --version > %WindowsBuildLocation%\VERSION.txt

REM --- Replace zipfile
del %WindowsBuildLocation%\ampersand.zip
%ZIP% a %WindowsBuildLocation%\ampersand.zip %AMPERSANDEXE%
%ZIP% a %WindowsBuildLocation%\ampersand.zip %WindowsBuildLocation%\VERSION.txt

REM-- Output 
dir %WindowsBuildLocation%\
echo .
type %WindowsBuildLocation%\VERSION.txt


```

If anyone else uses it, it should be adapted to have the right paths. I think the script speaks for itself. It assumes ampersand.exe has been built. Then it is called to produce a file containing it's version. Sourcetree has a 7za.exe, which can be used to compress the file. The compressed executable and the VERSION.txt file are in the zip file. Git can be used to update the master branch. 