`sh test.sh`
You pass test.sh as a parameter to sh.
`./test.sh`
The system calls out the interpreter program and feeds in the scripts contents.
So you will need a bang line(the very first line in the script and starts with #!). The rest part of the script will be passed to the program immediately after.

So you can run shell via `#!/bin/bash`. You can even run python via `#!/usr/bin/python` (the rest code is in python)

reference: https://askubuntu.com/questions/22910/what-is-the-difference-between-and-sh-to-run-a-script
