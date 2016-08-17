
# DocDown Format
v 1.0

---

## Directory Structure
The repository will contain the following files at the root level:

- `docs` This folder will be the root of the documentation.
- `LICENSE` The license for the documentation
- `config.json` Navigation structure and optional repo configuration

#### config.json
This file contains a dictionary of all sections and classes contained in the repository, in the order in which they will appear on the developer portal. It also allows the option to override the default language and default asset directory.

#### /docs
The root level of /docs contains an “assets” directory for storage of global assets, an “index.md” file for root-level content, and individual directories for each section or class. Directories can contain spaces.

Each directory in /docs can contain an “index.md”  which contains the documentation in the Markdown format as described below.

In addition to the Markdown file, assets like code samples, tables, and images, can be stored in an “assets” folder next to the index.md file. Supported files are listed in the [Importing Files](#importing-files) section.


When referencing assets, the parser will first look at the /assets directory at the same level as the “index.md” file. If the asset is not found, the parser will look up the directory tree until it reaches the global /assets directory. Assets cannot be shared across repositories.

![Example Directory Structure](https://github.com/smartdevicelink/sdl_markdown_spec/blob/master/assets/image01.png)

#### Nesting
Maximum pages level in hierarchy is 2 only.

Example:
```
docs \
	Level 1 \
		index.md
		level 2 \
			index.md
		level 2 \
			index.md
		...
	level 1 \
		index.md
	...
```

## Basic Markdown Syntax
#### Page headers
###### H1
**NOTE**: H1 is reserved for page titles and shouldn’t be used in the documentation
`#`

###### H2
Page Section Titles
`##`

###### H3
Sub-Section Titles
`###`

###### H4
Chart Titles
`####`

###### H5
Notes, Chart Column Titles
`#####`

###### H6
Chart Row Titles
`######`

#### Text Styling
###### Emphasis
`_emphasis_`, or `*emphasis*`

###### Strong
`__strong__`, or `**strong**`

###### Strikethrough
`~~strikethrough~~`

###### Inline Code
```
`code`
```

###### Block Code
> \`\`\`language
> Class = new className;
> \`\`\`

###### Blockquotes
Supports nested blockquotes
`>`

#### Lists
###### Unordered list
```
- List item 1
- List item 2
```

###### Ordered list
```
1. Item 1
1. Item 2
```

#### Links
###### Inline Link
`[link text](https://www.google.com)`
###### Inline Link + Title
`[link text](https://www.google.com “Title”)`

###### Reference Link
```
[link text][reference text]
---
[reference text]: https://www.google.com
```

#### Images
###### Inline Image
`![alt text](https://google.com/image.png "Title Text")`

###### Reference Image
```
![alt text][image]
---
[image]: https://google.com/image.png "Title Text"
```


####Tables
###### Table Structure
```
| Header           | Header 2           | Header 3           |
| ---------------- | ------------------ | ------------------ |
| cell content     | cell content       | cell content       |
```

###### Center align column
```
| Header           | Header 2           | Header 3           |
| :--------------: | ------------------ | ------------------ |
```


##### Right align column
```
| Header           | Header 2           | Header 3           |
| ---------------: | ------------------ | ------------------ |
```


#### Page Elements
###### Horizontal Rule
`---`

###### Line Break
```
Line 1 text
Line 2 text
```

##### Paragraph Break
```
Line 1 text

Line 2 text
```


## Extended Markdown Syntax
#### Notes
###### Generic Note
Fenced by !!!.  Supports inline markdown. Content can start on first line or new line. “NOTE” type is optional, as it is the default.

```
!!! NOTE
Content
!!!
```

###### Important Note
```
!!! IMPORTANT
Content
!!!
```

###### HMI Must
```
!!! MUST
Content
!!!
```

###### HMI May
```
!!! MAY
Content
!!!
```

###### Sequencing Charts
Link to Sequencing Chart

```
|||
Content
![alt text](assets/diagram.jpg)
|||
```


## Links
###### Link to another class
`[link text][Class Name]` or
`[link text][parent/ClassName]`
Links without a leading slash are treated as links between documents by the parser. The parent directory can be included to handle namespace conflicts.

###### Link to a specific version
`[link text][version/ClassName]`
If omitted, the latest version is used for the link

###### Link to a specific constant in a class or method
`[link text][version/Class Name/constant]`
`[link text][version/Class Name/method]`

###### Link between platforms
`[link text][platform/version/Class Name/constant]`
Allows the link to traverse repos (linking iOS to Core). Version and Constant are optional.

## Document Metadata
A document can begin with a metadata section defined by “---” with keys and values as shown below:

```
---
key: value
key2: value2
---
```

## Language Support
Localization of files is handled by appending the language code to the file itself. Directories currently cannot be localized. The default language is `_en_us` and is optional. Assets can be localized as well, in the same fashion.

## Importing Files
External code snippets can be imported and will be parsed using their native language. CSV imports will create HTML tables from their content. The parser will look in the assets/ directory for all imported files.

`+++ file.m`

`+++ response.json` would import a JSON code snippet from `assests/response.json`.

Supported file types:
* JSON
* CSV
* HTML
* JS
* CSS
* Obj-C
* Swift
* Java
* C++
