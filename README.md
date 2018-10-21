# GTK-List-ManifestDB-From-iOSBackup
Read and extract files from iOS backup made by iTunes ( C++ / Linux / Gnome / GTK / gtkmm )

Program for parsing the Backup files of iOS generated by iTunes for iPad and iPhone
<center>( See what is covered under the hood of iOS )</center>

The program was written in C++ with use of gtkmm wrapper for Gnome GTK environment of Linux.

The development environment in the moment is Netbeans IDE 8.2 under Fedora 28 Cinnamon. Alternatively you can easily compile and run the program in Terminal with the added shell script:

$ sh ./ManifestDBView.sh

The program follows the design of the earlier program List-ManifestDB-From-iOSBackup written in Swift (published in my repository). Since I switched from macOS to Fedora Linux (for what reasons ever) I had to change my programming language. For "simplicity" I choose C++ and to my pleasure found its "way to think" very similar to Swift and Objective-C. In some aspects I found C++ in combination with GTK easier compared to Swift ...

I wrote this program to become familiar with the C++ language, especially the GTK-API under the gtkmm wrapper and to get a feeling how to display multiple widgets on the screen. Take it as example for handling of windows, boxes, comboboxes, treeviews, textviews and more.

I am using a variadic function to compose display status messages in an extra TextView. The code for this is originated from</br>
<https://stackoverflow.com/questions/21806561/concatenating-strings-and-numbers-in-variadic-template-function>

I modified it for my needs ...

Background:
The file Manifest.mbdb describes no longer the backup files for iOS. Beginning with iTunes version 12.5 (or so) the main information for the files is stored in a SQLite database Manifest.db. iTunes of macOS Sierra is using this scheme in any case.

The structure of this database is as follows 
```
$ sqlite3
sqlite> .open Manifest.db
sqlite> .fullschema
CREATE TABLE Files (fileID TEXT PRIMARY KEY, domain TEXT, relativePath TEXT, flags INTEGER, file BLOB);
CREATE INDEX FilesDomainIdx ON Files(domain);
CREATE INDEX FilesRelativePathIdx ON Files(relativePath);
CREATE INDEX FilesFlagsIdx ON Files(flags);
CREATE TABLE Properties (key TEXT PRIMARY KEY, value BLOB);
.quit
```
Access to SQLite under C++ was realized analogous to</br>
&nbsp; <https://gist.github.com/zgchurch/3bac5443f6b3f407fe65>

Use the program for extracting of backuped files which could not be recovered otherwise.

Usage:
Click on "Open" left in the toolbar above to open an appropiate data base file. The Backup is structured in so-called domains. Choose a domain from the appearing Combobox and you will see further components of the backup. Double-clicking a row in the table opens a dialog where you can select the place for storing the requested file. If you know which domain entry you are looking for, enter a significant beginning of the text in the entry field of the combobox and press ENTER. This first entry which will match is then selected. Quit the program with "Quit".

Disclaimer: Use the program for what purpose you like, but hold in mind, that I will not be responsible for any harm it will cause to your hard- or software. It was your decision to use this piece of software.