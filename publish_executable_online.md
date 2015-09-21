# Publish ampersand.exe online

Currently, in the documentation there exists a link to ampersand.zip, as it is in the master branch of 

To create a zip file like that, you need to be on a windows machine. (there is no cross-compiler available as far as I know). 

I use the following batch file to create ampersand.zip:

```.sh
del C:\Git\webFiles\executables\windows\VERSION.txt
C:\Git\ampersand\.cabal-sandbox\bin\ampersand.exe --version > C:\Git\webFiles\executables\windows\VERSION.txt
del C:\Git\webFiles\executables\windows\ampersand.zip
"C:\Program Files (x86)\Atlassian\SourceTree\tools\7za.exe" a C:\Git\webFiles\executables\windows\ampersand.zip C:\Git\ampersand\.cabal-sandbox\bin\ampersand.exe
"C:\Program Files (x86)\Atlassian\SourceTree\tools\7za.exe" a C:\Git\webFiles\executables\windows\ampersand.zip C:\Git\webFiles\executables\windows\VERSION.txt
dir C:\Git\webFiles\executables\windows\
```

If anyone else uses it, it should be adapted to have the right paths. I think the script speaks for itself. It assumes ampersand.exe has been built. Then it is called to produce a file containing it's version. Sourcetree has a 7za.exe, which can be used to compress the file. The compressed executable and the VERSION.txt file are in the zip file. Git can be used to update the master branch. 