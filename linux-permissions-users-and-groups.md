# Linux Permissions, Users and Groups

#### Read, Write & Execute Permissions <a href="#read-write-and-execute-permissions" id="read-write-and-execute-permissions"></a>

Permissions are the “rights” to act on a file or directory. The basic rights are read, write, and execute.

* **Read:** a readable permission allows the contents of the file to be viewed. A read permission on a directory allows you to list the contents of a directory.
* **Write:** a write permission on a file allows you to modify the contents of that file. For a directory, the write permission allows you to edit the contents of a directory (e.g. add/delete files).
* **Execute:** for a file, the executable permission allows you to run the file and execute a program or script. For a directory, the execute permission allows you to change to a different directory and make it your current working directory. Users usually have a default group, but they may belong to several additional groups.

Permissions example:`-rw-r--r-- 1 root root 1031 Nov 18 09:22 /etc/passwd`

``![](<.gitbook/assets/image (4).png>)``

> The first ten characters show the access permissions. The first dash (-) indicates the type of file (d for directory, s for special file, and - for a regular file). The next three characters (rw-) define the owner’s permission to the file. In this example, the file owner has read and write permissions only. The next three characters (r--) are the permissions for the members of the same group as the file owner (which in this example is read only). The last three characters (r--) show the permissions for all other users and in this example it is read only. Some permissions may begin with d or l signifying that those permissions are for a directory or a link.

**Groups**:A user’s primary group (default group) is usually the group that is recorded in your Linux system’s /etc/passwd file. Linux system users can have a maximum of 15 secondary groups. A Linux system’s groups are stored in the /etc/group file.

**Sudo users:**

In order to provide a user with the sudo ability, they need to be added to a sudo enabled group, or their username needs to be added to the sudoers file with a set of permissions. This file is sensitive and important as an access and security control, and should not be edited directly with a text editor.

**Commands:**

* View Permissions: `ls -l <fileName/DirectoryName>`
* Find a user’s primary group information: `id <userName>` . If you want a less verbose output that only shows the primary group name: `id -gn <userName>`
* Find the groups of a user: `groups <userName>`
* Add a user to group/s: `sudo usermod -a -G <groupName> <userName>` . The -a and -G options ensure that the user is not removed from any group that the user already belongs to.
* Create a new standard user: `useradd <userName>`. Use the -e flag to set the date when the account expires: `useradd <userName>** -e <YYYY-MM-DD>`.
* Set a password for a user: `passwd <userName>`
* Remove a user account: `userdel <userName>`
* Remove the user, their home folder, and their files: `userdel -r <userName>`
* ``

mkdir -p \<directoryName/directoryName>(the -p flag creates a directory whether the first directory specified was created or not).

Create a softlink(symlink) ln -sf \<source> \<linkName>
