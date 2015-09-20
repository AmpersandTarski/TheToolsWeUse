# GitBook

[Gitbook](www.gitbook.com) is a tool to write documentation. The documentation you are reading at this very moment is created using GitBook. It allows to write the documentation in [Markdown](https://www.gitbook.com/book/gitbookio/markdown/details), which is an easy to use document-format.

The documentation is organized as a book. We prefer this over a traditional wiki, because a book contains a content part, which helps both author as well as the reader to think about structure, so everything can easily be found. Each book can be served as a (part of a) website, as well be downloaded in several forms, like pdf or e-book. We use a fully automated toolchain to build the book for each commit to the master branch of a book. 

At AmpersandTarski, we currently have two repositories, each dedicated to the documentation for a specific audience:

1. The repository [AmpersandTarski/TheToolsWeUse](https://github.com/AmpersandTarski/TheToolsWeUse) contains the contents of the book you are currently reading. You probably found it [here](https://www.gitbook.com/book/ampersandtarski/the-tools-we-use-for-ampersand/details). This document is not about Ampersand, but about the way Ampersand is being developed
2. The repository [AmpersandTarski/documentation](https://github.com/AmpersandTarski/documentation) is going to contain the documentation about Ampersand itself. 

## Getting started with GitBook
If you want to add to the documentation, it is possible to update the repository with any tool you like. However, we strongly advise to use the GitBook editor. A lot of cumbersome work is automated for you. Here are the steps to get on your way:
* Create an account at [Gitbook](www.gitbook.com). 
* Once you have an account get in touch with [Han Joosten](mailto://han.joosten.han@gmail.com) so he can grant you access to the book(s) you want to contribute to. 
* You will automatically find the books at your [Gitbook dashboard](https://www.gitbook.com/@ampersandtarski/dashboard), where you will find a button to start editing the book.

## The GitBook Web Editor
The editor explains itself. At GitBook, they eat their own dogfood to write [GitBook Documentation](http://help.gitbook.com/) .

## The GitBook desktop client
Recently, Gitbook also has a desktop client. It can be found [here.](https://www.gitbook.com/editor/)
When you install this desktop client, GitBook will make a local clone of the book. You will find it at ```~home/Gitbook```. As far as I know, this is not configurable, so you'll just have to deal with it. 
You can synchronize from within gitbook. However, if it gets a little bit complicated, I prefer sourcetree to give the correct git commands. 



### Writing Ampersand documentation using GitBook
1. Each time the master branch is committed, the book is generated. While we are in draft, it is a good idea to use a separate branch to do the writing, for each time you save your work in the editor, a commit is done to the github repo. ([see this info on draft workflow](http://help.gitbook.com/editor/draft.html)) 
2. 




