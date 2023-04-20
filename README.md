# Yoda_iCommand_workshop

## Outline

* Introduction
* Practical matters
* Configuring iCommands for Geo-YoDa
* Handson exercises

## Introduction
This workshop is designed for the beginner users to use the basics of iCommands in YoDa. The users should have access to an environment where iRODS is already installed before the workshop.
Here we provide a step-by-step guide to configure iRODS for Geo-YoDa and provide hands-on excercises to interact with YoDa via iCommands.

## Practical matters

### Data Access Password (DAP)
To access YoDa via iCommands you need to have a data access password. It is an alternative to the multi-factor authentication. To generate a DAP, follow the instruction below:

1. Login to the YoDa web portal
2. From the menu on the top-right, select data access password
3. Generate one and save it somewhere safe

### Accessing eejit and Snellius
We asume the attendance have access to either eejit or Snellius. To access to each of them you need to following procedure:
**eejit:**
To access eejit, run the command below in your terminal:

    ssh your_solis_username@eejit.geo.uu.nl

and enter your eejit password (your password will not be shown on the terminal as you are typing in or pasting).

**Snellius:**
To access Snellius, run the following command:

    ssh your_snellius_username@snellius.surf.nl
and then enter your Snellius paasword (your password will not be shown on the terminal as you are typing in or pasting).

### Loading iRODS madule on eejit and Snellius
If you use eejit or Snellius in the workshop, you can load iRODS madule easily via:

**eejit:**
Run the following commands:

    module load opt/all
 then
 
    module load iRODS/4.2.8

**Snellius:**

    module load 2021
then

    module load iRODS-iCommands/4.3.0
## Configuring iCommands for Geo-YoDa
After the iRODS madule is loaded, you need to configure the iRODS to interact with Geo-YoDa, To do that you need to follow the steps below:

**1. Find .irods/ directory**
When you are on eejit or snellius, your current directory is /home/username/. You can check it using

    pwd
which shows the current directory. If your current directory is /home/username/, then check if the .irods/ exist via:

    ls -a
if the ".irods" directory is in the list, go to the step 2, otherwise make it via:

    mkdir .irods
**2. make the iRODS config file**
If the .irods directory did not exist and you create it in the first step, you need to create and iRODS config file as well via:

    touch .irods/irods_environment.json

Then open the irods_environment.json file:

    nano .irods/irods_environment.json

and copy/past the following text block:

    {
    "irods_host": "geo.data.uu.nl",
    "irods_port": 1247,
    "irods_home": "/nluu11p/home",
    "irods_user_name": "exampleuser@uu.nl",
    "irods_zone_name": "nluu11p",
    "irods_authentication_scheme": "pam",
    "irods_encryption_algorithm": "AES-256-CBC",
    "irods_encryption_key_size": 32,
    "irods_encryption_num_hash_rounds": 16,
    "irods_encryption_salt_size": 8,
    "irods_client_server_negotiation": "request_server_negotiation"
    }
 
 then modify the 4th line and put your email address instead of exampleuser@uu.nl and save the file(using ctrl+x -> y -> press enter).

**3. Login to YoDa**
Now, you can login to YoDa via:

    iinit
and fill your **Data Access Password** where it is asked and press enter. If it does not show any error message, you have succefully logged in. you can test it by 

    ipwd
which should give you the current directory on YoDa (should be this : /nluu11p/home).

## Hands-on exercises

**Linux (shell) commands vs iCommands**

The commands in iRODS have the same logic as Linux commands. To start working with iCommands, it is recommended to have a basic undestanding of Linux (shell) commands. Here are few of them:

| Shell commands | Description |
| ------ | ------ |
| pwd | Show the current directory |
| cd <path-to-a-directory> | Navigate to a directory|
| ls | list of the files and folders in the directory |
| mkdir <name-of-directory> | Make a new directory |
| touch <name_and_format_of_the_file>| Make a new file |
| cp <path_to_the_file> <path_to_the_destination> | Copy a file to another directory (with cp -r it works for folders as well) |

Most of the the commands being used in iCommands are the same as Linux shell commands begining with an "i". For instance:

| iCommands | Description |
| ------ | ------ |
| ipwd | Show the current directory of iRODS/YoDa|
| icd <path-to-a-directory> | Navigate to a directory on iRODS/YoDa|
| ils | list of the files and folders in the directory in iRODS/YoDa |
| ... | ... |

You can find a list of the most used iCommands [here](iCommands_list.md).

### E1: Using the ihelp and help option

Get the list of iCommands using ihelp:

    ihelp
and then get information of one of the iCommands using the -h option; for instance:

    iget -h

### E2: Check your current directory on YoDa

Check your current directory and navigate to the workshop directory

    ipwd
    
and navigate to the workshop directory:

    icd /nluu11p/home/research-workshop
    
Check again your current directory using ipwd to make sure that you are there.

### E3: create your own sub-directory on YoDa

Now you are in the workshop directory, here make a sub-directory with test_yourname via the command below:

    imkdir test_yourname
    
Then navigate to the folder that you created using icd

### E4: Create a file on your local machine

You can create a file with a specific size via (follow the file_yourname convention):

    truncate -s 10M file_maisam.txt
    
and check if it is created with the given size:

    ls -lh file_maisam.txt    

### E5: Upload file to YoDa

Now, you can upload the file that you created to YoDa via:

    iput -fvP -N 16 file_maisam.txt /nluu11p/home/research-workshop/test_yourname
    
*To upload a folder to YoDa you need to add "r" to the options list*

### E6: Download data from YoDa

Let's download file from YoDa via:

    iget -fvP -N 16 /nluu11p/home/research-workshop/download_test.txt

*To download a folder to YoDa you need to add "r" to the options list*

### E7: Synchronize YoDa folder with local directory

Synching sometimes a good way to make sure that your data on YoDa is the same version as on your local storage:

Make a new folder on your local machine:

    mkdir sync_maisam
    truncate -s 5M sync_maisam/sync_file.txt

Then sync the new folder with you folder on YoDa

    irsync -rKv sync_maisam i:/nluu11p/home/research-workshop/test_maisam
