# Log Entry

**Learning the Command Line**

This is a backlog of notes from week 02.

* `ls` lists files and directories
* `pwd` displays the name of the directory you are currently in; stands for "print working directory"
* `mkdir` creates a file; stands for "make directory"
  *  When creating a file, it is case sensitive; do not use special characters; use dash, underscore, or camelcase for combining words 
* `rmdir` removes or deletes an **empty** file; stands for "remove directory"
  * Requires input; ex: `rm example_text.md`
* `cd` moves you to a different directory; stands for "change directory"
  * Requires input to go to a different directory; ex: `cd Images`
  * Use just `cd` to return to home directory
* `touch` changes a file's access and modification timestamp
  * Creates an empty file with input; ex: `touch data.csv`
* `echo` displays/prints a line of text to standard output
  * Can send text to file with input; ex: `echo "hello world" > data.csv`
* `cat` displays contents of a file; can concatenate multiple files
  * Requires input; ex: `cat data.csv`
  * `cat file1.txt file2.txt > file3.txt` would output contents of files 1 and 2 into file 3; if file 3 did not exist, it would be created
* `cp` copies files and directories
  * Generally takes two inputs; ex: `cp data.csv data.csv.bak`
* `mv` moves files and directories; another way of renaming files
  * Generally takes two inputs; ex: `mv data.csv data.old`
* `rm` removes/deletes a file/directory
