# Log Entry

**Learning the Command Line**

This is a backlog of notes from week 02.

* `ls` lists files and directories
* `pwd` displays the name of the directory you are currently in; stands for "print working directory"
* `mkdir` creates a file; stands for "make directory"
  *  When creating a file, it is case sensitive; do not use special characters; use dash, underscore, or camelcase for combining words 
* `cd` moves you to a different directory; stands for "change directory"
  * Requires input to go to a different directory; ex: `cd Images`
  * Use `cd` or `cd ~` to return to home directory
  * Use `cd /` to return to root directory
  * Use `cd ..` to go to parent directory; can string multiple dots to skip multiple directories; ex: `cd ../..`
  * Use `cd -` to return to the immediate prior directory that you were in
* `touch` changes a file's access and modification timestamp
  * Creates an empty file with input; ex: `touch data.csv`
* `echo` displays/prints a line of text to standard output
  * Can send text to file with input; ex: `echo "hello world" > data.csv`
* `cat` displays contents of a file; can concatenate multiple files
  * Requires input; ex: `cat data.csv`
  * `cat file1.txt file2.txt > file3.txt` would output contents of files 1 and 2 into file 3; if file 3 did not exist, it would be created
* `cp` copies files and directories
  * Generally takes two inputs; ex: `cp data.csv data.csv.bak`
  * Can copy and rename file; ex: `cp paper.txt Documents/paper.text.bak`
  * Can work in reverse; ex: `cp Documents/paper.txt.bak paper.txt` 
  * Can move file back to home directory using `~/`; ex: `cp Documents/paper.txt.bak ~/paper.txt`
* `mv` moves files and directories; another way of renaming files
  * Generally takes two inputs; ex: `mv paper.text Documents/`
  * Can move and rename file; ex: `mv paper.txt Documents/paper.text.bak`
  * Can work in reverse; ex: `mv Documents/paper.txt.bak paper.txt`
  * Can move file back to home directory using `~/`; ex: `mv Documents/paper.txt.bak ~/paper.txt``
* `rm` removes/deletes a file/directory
  * Requires input; ex: `rm Documents/paper.txt.bak`
* `rmdir` removes or deletes an **empty** file; stands for "remove directo>
  * Requires input; ex: `rm example_text.md`
* `rm -r` deletes a full directory
  * Requires input; ex: `rm -r Documents/notes`
* `date +%F` provides the current date in `year-month-day` format
  * Can create a file using this code; ex: `nano $(date +%F).md`
* `clear` will clear the screen in terminal
* bash completion will autofill file names
  *ex: if you only have one file starting with an`o`, you can type `o` and press tab to autocomplete the file name
  *ex: `grep "chrome" o` -> `grep "chrome" operating-systems.csv`
* Use the up arrow to autofill previous commands you have entered
