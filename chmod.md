chmod:Change the mode of each FILE to MODE.
1. `ls -l` the first column will show the permissions for files.
on each line, the first character identifies the type of entry that is being listed. If it is a dash(-), it is a file. If is the letter `d`, it is a directory.
The next 9 characters represent the settings for `user permissions`, `group permissions` and `other permission` (each 3 characters).
`User` is the one who owns the file.`Group` is the other users in the group(add the link to another article here). `Other` can be anyone not in the first two categories.
There are 3 characters in each set of permission. The character means:
1. `-`: Permission not granted.
2. `r`: Read permission. The file can be opened and its content viewed.
3. `w`: Write permission. Th filed can be edited, modified and delted.
4. `x`: Execute permissions. If the file is a script or a program (like a shell script), it can be executed.

add a picture here
The syntax for `chmod` is: `chmod <who><what><which> <file name>`
(put it to a table here)
`<who>`:
1. `u`: user, the owner of the file
2. `g`: group, members of the group the file belongs to
3. `o`: others
4. `a`: all above, anyone
If you do not specify `<who>`, `chmod` will take `a` as default.

`<what>`:
1. `-`: remove permission
2. `+`: add permission
3. `=`: set a permission and remove others

`<which>`:
1. `r`: read permission
2. `w`: write permission
3. `x`: execute permission

eg. `chmod u=rwx, og=r file.txt` `chmod +x scipt.sh` `chmod o-r *.txt`

Numerical Shorthand
- 0: no permission
- 1: execute
- 2: write
- 3: write & execute
- 4: read
- 5: read & execute
- 6: read & write
- 7: read & write & execute

https://www.howtogeek.com/437958/how-to-use-the-chmod-command-on-linux/




