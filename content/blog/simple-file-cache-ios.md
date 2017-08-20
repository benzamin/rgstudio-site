+++
categories = ["ios"]
date = "2017-08-20T12:38:01+06:00"
tags = ["ios", "programming"]
title = "Simple file caching & manipulation in iOS"
banner = "img/blog/ios-simple-filemanager.png"
+++

 >This document is heavily influenced by [Apple docs](https://developer.apple.com/library/content/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/AccessingFilesandDirectories/AccessingFilesandDirectories.html)

(Jump: Browse to the [sample code][githubref] on Github)<br>
For security purposes, an iOS app’s interactions with the file system are limited to the directories inside the app’s sandbox directory. During installation of a new app, the installer creates a number of container directories for the app inside the sandbox directory. Each container directory has a specific role. The bundle container directory holds the app’s bundle, whereas the data container directory holds data for both the app and the user. The data container directory is further divided into a number of subdirectories that the app can use to sort and organize its data. The app may also request access to additional container directories—for example, the iCloud container—at runtime.

<img src="https://developer.apple.com/library/content/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/art/ios_app_layout_2x.png" alt="iOS App Sandbox - Courtesy of Apple" style="width: 400px;"/>

An app is generally prohibited from accessing or creating files outside its container directories. One exception to this rule is when an app uses public system interfaces to access things such as the user’s contacts or music. In those cases, the system frameworks use helper apps to handle any file-related operations needed to read from or modify the appropriate data stores.

### Accessing Files and Directories

Before you can open a file, you first have to locate it in the file system. The system frameworks provide many routines for obtaining references to many well-known directories, such as the Library directory and its contents. You can also specify locations manually by building a URL or string-based path from known directory names.

When you know the location of a file, you can then start planning the best way to access it. Depending on the type of file, you may have several options. For known file types, you typically use built-in system routines to read or write the file contents and give you an object that you can use. For custom file types, you may need to read the raw file data yourself.

### BBFileManager Class
This small utility class let you do some basic things...

 + File caching with **expiration date** for Objects which implements NSCoding protocol.
 + File manipulation of image files, NSArray and NSDictionary.
 + Get file exists or not from documents directory, save and delete them.
 + All the methods are class methods, so no need to instantiate.

 Here is the class:
 <script src="https://gist.github.com/benzamin/206344e1b8a097c560cbc5eb400df63d.js"></script>


**Dont forget to explore and star my [github][hughubaccount] repos, comment if you have something in your mind 😊** 

 [githubref]:https://gist.github.com/benzamin/206344e1b8a097c560cbc5eb400df63d
 [hughubaccount]: https://github.com/benzamin/