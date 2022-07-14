# Linux Commands

1. Use `lshw ` (list hardware) to show the computer hardware information.

2. Use `uanme -a` to show system information.

3. `tar`

    ```shell
    tar –xvf file.tar # unzip .tar
    tar -xzvf file.tar.gz # unzip .gz
    tar -xjvf file.tar.bz2 # unzip .bz2
    tar –xZvf file.tar.Z # unzip .Z
    unrar e file.rar # unzip .rar
    unzip file.zip # unzip .zip
    ```

4. Show the structure of current directory.

    1. `sudo apt install tree`
    2. `tree -L N` show $N^{th}$ depth.

5. `#!/bin/bash` indicates the path to shell. It can only be placed at the top of shell script and begun with `#!`.

    1. `#!` is known as `shebang` in Unix.
    2. This command is used to instruct our system to use `bash` as default shell.

6.  `vim` `:set number` to show the line number.

7. `vim` comment out a block (in a shell script `#`)

    1. `:10,20s/^/#/g` to comment out a block from line 10 to 20
    2. `:10,20s/#//g` to delete the comments.

8. `vim` delete a line: click the line->exit Insert mode->double press d in your keyboard

9. How to calculate the time consumption of a shell script. Here is an example. Pay attention to the spaces in this script.

    ```shell
    #!/bin/bash
    startTime=`date +%s`
    for ((i=1; i<=100; i++)); do
            a=$[$i%20]
            if [ $a -eq 0 ]; then
                    echo "i: $i"
            fi
    done
    endTime=`date +%s`
    consumedTime=$[ $endTime - $startTime ]
    echo "Time consumed: $consumedTime seconds"
    ```

10. How to show the folder size in terminal. `du`: summarize disk usage of the set of files, recursively for directories.

    ```shell
    $ du -sh # show the size of current folder
    $ du -h # show the sizes of all subfolders/files (recurssively)
    $ du -h <folder name> # show the sizes of indicated folder/files
    ```

11. `find .|xargs grep -ri "characters you want to find"` search all files under current directory to find specific characters.

12. more ...

