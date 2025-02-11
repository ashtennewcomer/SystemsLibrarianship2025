# Log Entry

**Using grep**

* `-i` ignores case
  * grep is case sensitive by default
  * use `-i` to ignore case; ex: `grep -i "chrome" operating-systems.csv`
* `-v` inverse search
  * returns lines that do not match search criteria
* `head -n1` will return only the first line of the file
  * the number can be changed to adjust the number of lines returned
* `^` regex indicating the beginning of a line
  * ex: `grep -i "^os" operating-systems.csv` will return everything in the file that begins with `ov`
*  `$` regex indicating the end of a line
  * ex: `grep -i "year$" operating-systems.csv` will return everything in the file ending with `year`
* `-c` counts the number of lines containing search criteria
  * ex: `grep -ic "proprietary" operating-systems.csv`
`|` inflix operator acts as OR boolean operator
  * ex: `grep -EI "(bsd|gpl|apache)" operating-systems.csv`
* `-w` searches for the string only as a complete word
* `-A#` prints matching line + specified number of lines after
* `-B#` prints matching line + specified number of lines before
* `-#C` prints matching line + specified number of lines before and after
* `-m#` returns a search for the string and stops after the specified number of results
* `-n` will print the line number for each hit
* `[a-z]{#}` searches for any word with specified # of letters or more that contains any English character between `a-z`
* `[0-9]{#}` searches for any word with specified # of letters or more that contains any number between `0-9` 
* `"letter.{#}letter"` searches for words that begin and end with the specific letters and amount of characters in between
  * ex: `grep -Eiw "m.{3}s" operating-systems.csv`
* Save grep output by adding `> file_name.txt` at the end of a command
  * ex: `grep -i "Journal" operating-systems.csv | sort | uniq -c > grep_output.txt`
* grep commands can be combined
  * commands with a # need to be at the end; ex: `-iwm1`
