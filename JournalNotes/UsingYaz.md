# Log Entry

**Using yaz**
 
Yaz is an information retrieval client that uses protocols to query bibliographic databases.

To install: `sudo apt install yaz`

Manual page: `man yaz-client`
Bibliographic attributes page: `man bib1-attr`

Running yaz:
* `yaz-client`
* open `library server address`
  * UK's address: `saalck-uky.alma.exlibrisgroup.com:1921/01SAA_UKY`

Searching with yaz:
* `find` search request
* `@and` Boolean AND search
* `attr 1=?` signifies the field to search
  * `1=1` personal name field
  * `1=4` title field
  * `1=21` subject heading field
  * `1=1016` any field
* `show #` displays the result record
  * `show 1 + # of results to show all records
* `ctrlL` clear screen
* `ctrlC` exit yaz client
* `file` prints file type
* `read` prints first few lines of file

Advanced Usage
* `yaz-client -m records.marc`
  * `records.marc` is the file name
* open `library server address`
* complete a search
* show specific or all records
* `quit`
* `head records.marc`
* `file records.marc`
  * should return `records.marc: MARC21 Bibliographic`
* `yaz-marcdump -o json records.marc > records.json`
* `jq . records.json > records-formatted.json`
* `less records-formatted.json`
* use jq command to examine specific fields in the JSON-formatted MARC records
* `json` converts files to a standard text-based format for representing structured data
* `jq` formats json for better readability
  * [jq tutorial] (https://jqlang.org/tutorial/) 

