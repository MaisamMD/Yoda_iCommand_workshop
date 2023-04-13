# Yoda_iCommand_workshop

## Outline

* Introduction
* Practical matters
* Configuring iCommands for Geo-YoDa
* Hands-on exercises

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

    module load iRODS/4.2.8

**Snellius:**

    module load 2021
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
