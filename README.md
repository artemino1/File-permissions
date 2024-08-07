<h1>File permissions</h1>

<h2>Description</h2>

In this scenario, we must examine and manage the permissions on the files in the `/home/researcher2/projects` directory for the `researcher2` user. The `researcher2` user is part of the `research_team` group. We must check the permissions for all files in the directory, including any hidden files, to make sure that permissions align with the authorization that should be given. When it doesn't, we must change the permissions.

<h2>Language Used</h2>

- <b>Bash</b>

<h2>Environments Used</h2>

- <b>Linux</b>

<h2>Program walk-through</h2>

Here’s how we’ll do this task: First, we’ll check the user and group permissions for all files in the `projects` directory. Next, we’ll check whether any files have incorrect permissions and change the permissions as needed. Finally, we’ll check the permissions of the `/home/researcher2/projects/drafts` directory and modify these permissions to remove any unauthorized access.

<h3>Check file and directory details</h3>

Commands for the following data will be (the result is enclosed):
-	`cd projects` (switch to the `/home/researcher2/projects` directory);
-	`ls -la` (reveals the content of current directory with the owner types of user, group, other with their rights to read/write/examine. In addition to that, the hidden file `.project_x.txt` is also disclosed:

![Check file and directory details](https://imgur.com/Z4Eq1VL.png)

<h3>Describe the permissions string</h3>

In the `/home/researcher2/projects` directory, there are five files with the following names and permissions: 

`project_k.txt`
-	User = read, write 
-	Group = read, write
-	Other = read, write
  
`project_m.txt`
- User = read, write
-	Group = read
-	Other = none
  
`project_r.txt`
-	User = read, write
-	Group = read, write
-	Other = read

`project_t.txt`
-	User = read, write
-	Group = read, write
-	Other = read
  
`.project_x.txt`
-	User = read, write
-	Group = write
-	Other = none

There is also one subdirectory inside the `projects` directory named `drafts`. The permissions on `drafts` are:
- User = read, write, execute
-	Group = execute
- Other = none
  
<h3>Change file permissions</h3>

The organization does not allow other to have write access to any files. Permissions of the `project_k.txt` were changed (the owner type of other doesn’t have write permissions) - `chmod o-w project_k.txt`:

`project_k.txt`
-	User = read, write 
-	Group = read, write
-	Other = read, ~~write~~

<h3>Change file permissions on a hidden file</h3>

The research team has archived `.project_x.txt`, which is why it’s a hidden file. This file should not have write permissions for anyone, but the user and group should be able to read the file. We use a Linux command to assign `.project_x.txt` the appropriate authorization.

First, we check the changes to the permissions in the `/home/researcher2/projects` directory:
`ls -la`. 
We change the permissions of the file `.project_x.txt` so that both the user and the group can read, but not write to, the file - `chmod u-w,g-w,g+r .project_x.txt`:

`.project_x.txt`
-	User = read, ~~write~~
-	Group = ~~write~~, ${\color{green}read}$
-	Other = none 
<h3>Change directory permissions</h3>

The files and directories in the `projects` directory belong to the `researcher2` user. Only `researcher2` should be allowed to access the `drafts` directory and its contents. 
First, we check the permissions of `/home/researcher2/projects/drafts` directory: `ls -l`
We remove the execute permission for the group and therefore has access to the `drafts` directory: `chmod g-x drafts`

The permissions on `drafts` are:
-	User = read, write, execute
-	Group = ~~execute~~
-	Other = none

<h2>Summary</h2>

We showed practical experience in using basic Linux Bash shell commands to:
-	examine file and directory permissions
-	change permissions on files
-	change permissions on directories



