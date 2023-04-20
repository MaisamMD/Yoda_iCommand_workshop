# Basic iCommands
Here we provide a list of the most useful iCommands
## Login: 

**iinit** 
Starts an iRods session (cwd) 

    iinit [-ehvVl] 

Optional arguments:  

-e &emsp; &emsp; echo the password as you enter it (normally there is no echo)

-l &emsp; &emsp; list the iRODS environment variables (only)

-v &emsp; &emsp; verbose

-V &emsp; &emsp; very verbose

-h  &emsp; &emsp; open the help menu for this command

This command will normally be replied with ‘Enter your current iRODS password.

>For YoDa, please enter your Data Access Password, which you have generated in the YoDa web portal. For more information how to create one, consult this manual;
https://geo-data-support.sites.uu.nl/manuals/yoda/dap/ 

**iexit**
Exits the iRODS session

    iexit [-vVh] 

Optional arguments: 

-v  &emsp; &emsp; verbose 

-V  &emsp; &emsp; very verbose 

-h  &emsp; &emsp; this help 

**ihelp**

Display iCommands synopsis or a particular iCommand help text 

    ihelp [-ah] [icommand] 
 
Optional arguments: 

-h &emsp; &emsp; this help 

-a &emsp; &emsp; print the help text for all the iCommands 

Run with no options displays a synopsis of the iCommands 

## Folders navigation

**ils**

Display the file and folders of a directory in YoDa-iRODS

    ils [-alr]

Optional arguments: 

-a &emsp; &emsp; show hidden files/folders

-l &emsp; &emsp; long format

-r &emsp; &emsp; recursive - show subfolders

For other optional arguments, please consult: https://docs.irods.org/master/icommands/user/#ils  

**ipwd** 

Shows your iRODS Current Working Directory. 

    ipwd [-v]

Optional arguments:

-v &emsp; &emsp; verbose 

**icd**

Changes iRODS the current working directory. If no directory is entered, the cwd is set back to your home directory as defined in your .irodsEnv file. In addition, by using icd .. you can move up one level.

    icd [-vh] <path to the directory>

Normally there is no need to use the optional arguments for this command.
 

## File transfer to/from YoDa-iRODS 

**iput**

Store/upload file/folders into YoDa-iRODS 

    iput [-rfvkP] [-N NumberOfThreads]  <source_file/folder> <dest_directory> 

There are several optional arguments that the upload iCommand iput can take. The most important ones are:

-r &emsp; &emsp; for recursive transfer of directories and their contents

-f &emsp; &emsp; force to upload file, overwriting file even if it exists

-v &emsp; &emsp; show information about uploading, e.g, duration of upload

-k &emsp; &emsp; calculate checksum on the data server-side

-P &emsp; &emsp; output the progress of upload

-T &emsp; &emsp; to renew socket connection after 10 mins (this may help connections that are failing due to some connection/firewall settings)  

-N &emsp; &emsp; upload data in number of threads (N) to increase the upload speed; 0 means no thread; of this option not used iRODS decide how many threads needed. Maximum number of threads is 16.

For other optional arguments, please consult: https://docs.irods.org/master/icommands/user/#iput 


**iget**

Get data-objects or collections from iRODS space 

    iget [-rfvKP] <source_file/folder> <dest_directory> 

There are several optional arguments that the upload iCommand iget can take. The most important ones are; 

-r &emsp; &emsp; for recursive transfer of directories and their contents

-f &emsp; &emsp; force to download file, overwriting file even if it exists

-v &emsp; &emsp; show information about uploading, e.g, duration of download

-K &emsp; &emsp; calculate checksum on the data server-side

-P &emsp; &emsp; output the progress of download

-T &emsp; &emsp; to renew socket connection after 10 mins (this may help connections that are failing due to some connection/firewall settings)  

-N &emsp; &emsp; upload data in number of threads (N) to increase the download speed; 0 means no thread; of this option not used iRODS decide how many threads needed. Maximum number of threads is 16.

For other optional arguments, please consult: https://docs.irods.org/master/icommands/user/#iget 

**irsync**

Synchronize entire directories between Yoda and other systems  

    irsync [-rKsV] <source_file/folder> <dest_directory> 

Keep in mind that this command is used for syncing on both ends and also between two folders on YoDa. Therefore, to make sure that it is clear for system, the folder on YoDa will be specified with an "i:" before the path. For example synchronizing data from local folder1 to folder2 on YoDa:

    irsync -r folder1 i:folder2
On the other way around, synchronizing data from folder2 on YoDa to local folder1:

    irsync -r i:folder2 folder1
and synchronizing data from folder1 to folder2 on YoDa:

    irsync -r i:folder1 i:folder2

There are several optional arguments that irsync can take. The most important ones are;

-r &emsp; &emsp; recursive - store the whole folder including subdirectories

-K &emsp; &emsp; Calculate and verify the checksum on the data

-s &emsp; &emsp; use the size instead of checksum

-v &emsp; &emsp; verbose 

For other optional arguments, please consult: https://docs.irods.org/master/icommands/user/#irsync 

**irm**

Remove one or more data-object or collection from iRODS space 

    irm [-rf] <file or folder on yoda> 

There are several optional arguments that the  iCommand irm can take. The most important ones are;

-r &emsp; &emsp; to remove entire folder and subfolders

-f &emsp; &emsp; permanently remove files/folders

*By default, the data-objects are moved to the trash collection (/myZone/trash) unless either the -f option or the -n option is used.*

For other optional arguments, please consult: https://docs.irods.org/master/icommands/user/#irm 

**imkdir**

Make a new directory on YoDa

    imkdir [-vp] <name of folder> 

-v &emsp; &emsp; output the details

-p &emsp; &emsp; make parent directories when needed
