---
description: Permissions, Users and Groups
---

# Linux

<details>

<summary>Read, Write &#x26; Execute Permissions</summary>

Permissions are the “rights” to act on a file or directory. The basic rights are read, write, and execute.

* **Read:** a readable permission allows the contents of the file to be viewed. A read permission on a directory allows you to list the contents of a directory.
* **Write:** a write permission on a file allows you to modify the contents of that file. For a directory, the write permission allows you to edit the contents of a directory (e.g. add/delete files).
* **Execute:** for a file, the executable permission allows you to run the file and execute a program or script. For a directory, the execute permission allows you to change to a different directory and make it your current working directory. Users usually have a default group, but they may belong to several additional groups.

![](<.gitbook/assets/image (3).png>)

Permissions example:`-rw-r--r-- 1 root root 1031 Nov 18 09:22 /etc/passwd`

The first three characters are for the user, the next three are for the group, and the last three are for others. The first ten characters show the access permissions. The first dash (-) indicates the type of file (d for directory, s for special file, and - for a regular file). The next three characters (rw-) define the owner’s permission to the file. In this example, the file owner has read and write permissions only. The next three characters (r--) are the permissions for the members of the same group as the file owner (which in this example is read only). The last three characters (r--) show the permissions for all other users and in this example it is read only. Some permissions may begin with d or l signifying that those permissions are for a directory or a link.

![](<.gitbook/assets/image (3) (1).png>)

The first column with the ten letters and dashes shows the permissions of the file or directory. The second column (with the single number) indicates the number of files or directories contained in the directory. The next column indicates the owner, followed by the group name, the size, date, and time of last access, and finally the name of the file.



Alternatively, numbers can be used to grant permissions as well

​![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F8HdAqUUy3RShZPGhf9ej%2Fuploads%2FiJulL3u4brXqueNiir1x%2Fimage.png?alt=media\&token=95e6bd50-34ca-4518-8d8a-eaf52ad7749c)​

So, for example:

* 777 is the same as rwxrwxrwx
* 755 is the same as rwxr-xr-x
* 666 is the same as rw-rw-rw-
* 744 is the same as rwxr--r--

![](<.gitbook/assets/image (4).png>)

#### Commands:

* View Permissions: `ls -l <fileName/DirectoryName>`
* Change permissions: `chmod +/- <permissions> <filename and/or directory>`

</details>

<details>

<summary>Ownership</summary>

Chown command lets you change the file owner and group through the command line.

#### Commands:

* Change the owner of a file: `chown <newOwner> <fileName>`
* &#x20;Change the group of a file: `chown :<groupName> <file-name>`
* Change both the owner and the group of a file: `chown <newOwner>:<newGroup> <fileName>`.  Alternatively the userId and groupId can be used instead. `e.g chown 1000:1001 test1`
* Change ownership on directory: `chown -R <newOwner>:<newGroup> <directory-name-or-path>`
* Change ownership after checking existing owner and/or group: `chown --from=[curr-own]:[curr-group] [new-owner]:[new-group] [filename]`
* Change ownership verbose: chown `<newOwner>:<newGroup> <fileName> -v`

</details>

<details>

<summary>Groups</summary>

A user’s primary group (default group) is usually the group that is recorded in your Linux system’s /etc/passwd file. Linux system users can have a maximum of 15 secondary groups. A Linux system’s groups are stored in the /etc/group file.

#### Commands:

* List all members of a group: `getent group developers`
* List all groups: `less /etc/group`
* Find a user’s primary group information: `id <userName>` . If you want a less verbose output that only shows the primary group name: `id -gn <userName>`
* Find the groups of a user: `groups <userName>`
* Create a new group: `groupadd <groupName>`
* Delete a group: `groupdel <groupName>`
* Switch groups: `newgrp <groupName>`
* Add a user to group/s: `sudo usermod -a -G <groupName> <userName>` . The -a and -G options ensure that the user is not removed from any group that the user already belongs to.

</details>

<details>

<summary>Sudo Users</summary>

In order to provide a user with the sudo ability, they need to be added to a sudo enabled group, or their username needs to be added to the sudoers file with a set of permissions. This file is sensitive and important as an access and security control, and should not be edited directly with a text editor.

```
# User privilege specification
root    ALL=(ALL:ALL) ALL
sudousername   ALL=(ALL:ALL) ALL
username ALL=/usr/bin/top, /usr/bin/apt-get
# Allow members of group sudo to execute the less, ls, and apt commands
%sudo ALL=/usr/bin/less, /usr/bin/ls, /usr/bin/apt
```

When whitelisting individual commands using the above syntax, it is important to use the absolute path to the command. The `which` command can be used to find this absolute path: `which command-name`

</details>

<details>

<summary>Find</summary>

**find command** can be used in a variety of conditions like you can find files by **permissions**, **users**, **groups**, **file types**, **date**, **size**, and other possible criteria.

#### Commands:

* Find files in directory based on name: `find /<directoryName> -name <fileName>`
* Find files by name, ignoring case: `find / -type d -name <directoryName>`. Type can be directory (d), file (f) etc.
* Find all files of specific extension:  `find / -type f -name "*.<extension>"`
* Find files based on permission: `find / -type f -perm <permission> -print`
* Find files not matching a permission: `find / -type f ! -perm <permission>`
* Find read-only files: `find / -perm /u=r`
* Find executable files: `find / -perm /a=x`
* Find directory and give permissions: `find / -type d -perm <permission> -print -exec chmod <permission> {} \ ;`
* Find file and remove: `find . -type f -name "<fileName>" -exec rm -f {} ;`
* Find all empty files: `find / -type f -empty`
* Find all hidden files: `find / -type f -name ".*`"
* Find all files based on a user: `find / -user <userName>`
* Find all files based on a group: `find / -group <groupName>`
* Find files modified in the last N days: `find / -mtime <numberOfDays(N)>`
* Find files accessed in the last N days: `find / -atime <numberOfDays>`
* Find files modified in between a set of days: `find / -mtime +<minDay>  –mtime  -<maxDay>`
* Find changed files in the last hour: `find / -cmin -60`. Use -mmin for modified files and -amin for accessed files.
* Find files of a specific size: `find / -size <size e.g 100MB>`
* Find files in home directory: `find ~ -name '*<extension>'`

</details>

<details>

<summary><strong>General Commands</strong></summary>

* Create a new standard user: `useradd <userName>`. Use the -e flag to set the date when the account expires: `useradd <userName>** -e <YYYY-MM-DD>`.
* Set a password for a user: `passwd <userName>`
* Remove a user account: `userdel <userName>`
* Remove the user, their home folder, and their files: `userdel -r <userName>`
* Create a directory: `mkdir <directoryName>`
* Create a directory and set permissions: `mkdir -m a=rwx <directoryName>`
* Create a nested directory: `mkdir -p <directoryName/directoryName1>`. The -p flag creats a directory whether the first specified has been created or not.
* Remove a file: `rm <fileName>`
* Remove a directory: `rm -r <directoryName`>
* View files and permisions: ls -l
* View files including hidden: ls -a
* View files including hidden and permissions: ls -al
* Change user: `su - <userName>`
* Create file: `touch <fileName>`
* List all users: `less /etc/passwd`

</details>

Create a softlink(symlink) ln -sf \<source> \<linkName>
