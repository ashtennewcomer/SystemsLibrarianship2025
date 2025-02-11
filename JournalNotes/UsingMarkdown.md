# Log Entry

**Using Markdown**

This is a backlog of notes from week 03. 

```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```
* **Bold**: wrap text in double asterisks/underscores to make it bold

* *Italic*: wrap text in single asterisks/underscores to make italicize text

* Use indention (2 spaces; not tab) to create sub-items in a list:
```
* Item 1
* Item 2
  * Subitem 1
  * Subitem 2
```
* Use numbers followed by periods for an ordered list:
```
1. First item
2. Second item
  1. Subitem 2.1
  2. Subitem 2.2
```
* **Links**: to create a named link, wrap the link text in brackets `[ ]`, and then wrap the URL in parentheses `( )`
  * ex: `[GitHub] (https://github.com)`
* **Images**: similar to links, but start with an exclamation mark, followed by alt text in brackets and the URL in parentheses
  * ex: `![Alt text](image-url.jpg)`
  * the image file must be in the same directory as the markdown file; use a relative path to link the image
    * ex: `[Alt text](images/image-url.jpg)` where `images/` is the directory name and `image-url.jpg` is the image file name
* **Inline Code**: use a single backtick to wrap your code in text
  * ex: \`inline code\`
* **Code Blocks**: for larger sections of code, use three backticks or indent with four spaces
  * ex: \```
    your code here
    \```
* **Blockquotes***: to create a blockquote, use the greater than symbol `>` at the beginning of a line; for nested blockquotes, use multiple `>` symbols
* **Horizontal Lines**: create a horizontal line by using three or more asterisks/dashes/underscores
* **Escaping Markdown**: display a markdown character by preceding it with a backslash `\`
  * ex: ` \*demo italicizing\* `
* Paragraphs are automatically created when text is separated by an empty line; create a new line without starting a new paragraph by ending a line with two or more spaces
