## JSON, YAML, TOML what are these strange letters mean?
All of these abbreviations are referred to data serialization formats
Later I will explain this term meaning.

So before we start I would like to tell what we will be doing for the next 10 minutes

Our goals for today's lecture:
1. Get to know what is JSON, YAML, TOML
2. Learn their main features
3. Find differences between them
4. after that we are going to compare them and understand which format is the best and why

Let’s start!

# JSON
***JavaScriptObjectNotation*** - is a language-independent, text-based representation of structured data based on JavaScript.
It was developed by Douglas Crockford in the ***2000***
Files which use JSON have an extension - ***.json***

Json is the oldest format of those that will be discussed today, so using it as an example, we will learn some basic concepts of data serialization formats.

### Why do we need JSON?
To understand the usefulness and importance of data serialization formats, i will tell you a bit about the history of interactivity on the web. Earlier, when a user clicked on a link or a button on the page, a request would be sent to the server, the server would prepare the information needed as HTML, and the browser would render the HTML as a new page. This pattern requiring the browser to re-render everything on the page even if only a small detail had changed. It was costly, that’s why the new technologies were developed. Instead of reloading the entire contents of the page, clicking the button would trigger a web request that would load in the background. When the contents were loaded, the data could be manipulated, saved, and displayed on the page using JavaScript.
So we need JSON:
- For store data in some order
- For data transmission (between a web browser or application client and a server, or between different servers)
- For human redable data format of these actions.

### Supported types
- string
- number
- boolean
- null
- object (special JSON object)
- Array

### Non supported types
- function
- Date
- undefined
(values of this types will be converted to string)

I want to mention we are not talking about javascript data types, but rather about entity types that we can use in JSON

### DATA exchange
1. For example, you want to change your name in your account of some social network
2. You would open editing window, type a new name and click on the button “Save”
3. Data (your personal id, new name and other necessary data) would be converted to JSON format (string) using the built-in method JSON.stringify()
4. Special JSON string would be passed to the server (which could be written in any programming language)
5. Server would receive JSON and, using special parsing method, convert it to required data format
6. Server would manipulate received data and give the response
7. Response would be converted to JSON and send to the client 
8. Client would receive JSON and convert it to required data and re-render page

The process of conversion of data to JSON called serialization
The reverse process is called deserialization.

### Compare XML and JSON
There are 2 pictures. You can see how the same data looks at XML (on the left side) and JSON (on the right side) formats
It’s obvious that JSON is more compact and understandable

### JSON advantages
- Human-readable
- Compact (requires less memory space)
- Fast 
  - has only 2 built-in required method,
  - due to the string form, JSON data can be easily transmitted through any communication channel
- Support arrays
- Unique way to exchange data between different domens
- Supported by wide range of different services
- Language-independent (JSON is based on the object notation of the JavaScript language. However, it does not require JavaScript to read or write it)

### JSON drawbacks
1. No schema (schema is the organization or structure for a database)
  - total flexibility to represent the data in any way you want
  - you could accidentally create misshapen data very easily
2. Only one number type (the double-precision floating-point format)
  - you cannot take advantages of the different number types available in many programming languages (double, float, integer, byte, short, long)
3. No comments
  - This requires additional documentation and increasing the risk of misunderstanding
4. No Date type
  - JSON has only 2 variants of Date representation:
    1. as string
    2. as number of milliseconds since the January 1, 1970
5. Verbosity
6. No way to reduce sections of repeated code (no variables)
  - can't create or use external variables
7. Values cannot be overridden

Ok, these drawbacks are really significant, so what alternative we can choose?

# YAML
**YAML** - firstly was said to mean ***Yet Another Markup Language***, but later was renamed as ***YAML Ain't Markup Language*** to distinguish its purpose as data-oriented, rather than document markup
It was developed by Clark Evans in ***2001***
YAML is more frequently used as a format for configuration files
YAML filenames use the extensions ***.yaml*** or ***.yml***

### SUPPORTED TYPES
1. Scalars
  - String
  - Numeric types:
    - Integer
    - Float
    - Boolean
2. Lists
3. Dictionaries

### Syntax
Common syntax features:
- Indentations are required
  - Separate data on "levels"
  - Only spaces are used, tabs are not allowed
-Multiple documents within a single stream are separated by three hyphens (---)

***KEY/VALUE PAIRS SYNTAX***
Compound keys (which consists of 2 and more words) can use a space, however this syntax variant is not recommended

***STRINGS***
If string contains some special character like _ or @, you will need quotes
A question mark in front of a key ("?key: value") allows the key to contain some special characters without quotes
Strings are delimited with indentation with optional modifiers to preserve (|) or fold (>) newlines

***COMMENTS***
To write a comment, you can use # followed by your message
Comment can start anywhere on a line and continue until the end of the line
Comments must be separated from other tokens by whitespace characters

***LISTS***
For representing lists in YAML you can use arrays and markdown-like syntax (use indentations and hyphens)

***DICTIONARIES***
A dictionary is represented in a simple key/value form (the colon must be followed by a space)

***ANCHOR***(variable or reference)
It is one of the most important feature. It helps avoid unnecessary code repetition.
An ampersand symbol (&) is used to create anchor, and an asterisk(alias) (*) is used to insert it.

### YAML'S ADVANTAGES
- Language-independent
- More human-readble
- Has Anchors (variables or references)
- Has Comments
- Has Multiline input

### YAML'S DRAWBACKS
- Need special parser-package
- The parsers are younger than JSON's and known to be less secure
- YAML is mainly designed for configuration files, when use for data interchange, many of YAML's features lose their appeal

# TOML
***TOML*** - Tom’s Obvious, Minimal Language
Is was developed by Tom Preston-Werner in ***2013***
TOML filenames use the extension .toml
TOML's syntax primarily consists of key = "value" pairs, [section names], and # comments

### SUPPORTED DATA TYPES:
- String
- Integer
- Float
- Boolean
- Datetime
- Array
- Table (hash-table)

Before comparing all, what we've learned today we need to define some ideal criteria by which we can compare our formats

### WHAT WE WANT FROM IDEAL SERIALISATION/DESERIALISATION FORMAT?
- It would be human-readble
- It would require a little space
- It would be easy to edit and write code (comments, variables)
- It would be easy to install in the project (built-in methods)
- It would be supported by different languages and interfaces
- It would have high security level

| Criteria/Name | JSON | YAML | TOML |
| ------------- | ---- | ---- | ---- |
| human readble | +    | ++   | ++   |
| memory space  | +    | +++  | ++   |
| comments      | -    | +    | +    |
| variables     | -    | +    | -    |
| security      | ++   | +    | +    |
| supportion    | - all languages | - all languages | - all languages |
|								|	- suitable for configuration files | - IDEAL for configuration files    | - IDEAL for configuration files    |
|								|	- suitable for data exchanging     | - NOT suitable for data exchanging | - NOT suitable for data exchanging |
| special features | - NO comments | - comments | - comments |
|                  | - NO variables | - anchors | - NO variables |
|                  | - lack of types | - strings without quotation marks | - indentation (tabs and/or spaces) is allowed but not required |
|                  | - No Date supportion | - No Date supportion | - Supports Date |
