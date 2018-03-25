# user management

## /etc/passwd
+ contains the users database
+ can be replaced with LDAP in large env

## /etc/shadow
+ contains real encrypted passwords if in the /etc/passwd second field is x

## /etc/login.defs
+ contains many rules related to login process


## finger <user>
+ allows for seeing user's private data: name, address
___
```sh
finger root 
```
___
## chfn 
+ allows for update of user's private data: name, office address, phone, etc.
___
```sh
chfn
```
___
## /etc/shels 
+ contains the limited by root available shels, e.g.: bash, sh, ksh, tcsh etc.
___
## chsh 
+ allows for change of user's shell: bash, sh, ksh, tcsh etc.
___
```sh
chfn
```
___
## /etc/group 
+ contains the list of groups, with GID and added users
___

## useradd <user>, usermod
+ adds user entry to /etc/passwd
+ adds user group entry to /etc/group
+ creates /home/user
+ creates user mail and his mail directory, email alias
+ uses /etc/login.defs and /etc/default/useradd files
+ -c specify user friendly name
+ -d specify different than default user's home dir
+ -g specify different primary group than default user's primary group
+ -G add the user to a supplementary group
+ -s specify user's shell
+ -m moves files from home dir to a new one
+ the options can be used in usermod command
```sh
useradd -D - presents default settings used when user account is created
```
___
## adduser <user> - in UBUNTU
+ perl script with additional functionalities
+ uses /etc/adduser.conf as a configuration file
___
## environment files
+ bash uses .bash_profile and .bashrc
+ ksh uses .profile
+ .vimrc for custimizing vim environment
+ the files are in /etc/skel dir, and are copied to users home dirs when their accounts are created
+ /etc/profile is executed before any user startup file, so god place to set system-wide environemnt variables
___
## userdel or deluser in UBUNTU - is a wraper for userdel
+ deluser uses /etc/deluser.conf
  + remove user's home dir
  + backup user's files
  + remove all files owned by the user
  + delete the user's group if emty
+ you must be shore that all processes related to the deleted user are removed from crontab
___
## lock and unlock the user
```sh
usermod -L user - locks user account
usermod -U user - unlocks user account
```
___
