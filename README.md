# con
Compactable Object Notation for a descriptive event log files that can be validated, viewed as markdown and optionally leave out redundant field data. Inspired by Markdown, JSONIC, MSON and CSV.

**Mimetype:** `text/x-con`

## Markdown Notation

```
# Object_Name
Object description
> metakey: metadata value

- [TYPE] key [alias] `[type] [from..to] [required]` [regex] [:value]
---  begins with `---` to end markdown notation
```

Where
- `# Object_Name` names the object (for schema mapping), also required to start markdown form of the notation
- `- [TYPE] ...` defines a custom type
- `- key [alias]` defines a key with an optional alias, ex `- address addr`
- `type` defines the type of the object value, defaults to safe_string
- `from..to` defines the min & max values (for numerics) and lengths for strings
- `required` if the field is required
- `regex` validation regular expression
- `value` value

## Default Meta Data values
Value seperator: ex: options could be `;` `|` or `\t` for tab

> seperator: ,

Newline seperator: ex: options could be `\l\n` or say `~n~` if you wanted to support \n in json data

> newline: /n

## JSON Notation
Line begins with `{` or `[` and contains the JSON data ending with the matching `]` or `}`

## JSONIC Lite Notation
Like JSONIC except limited to flat objects. Where , is the defined seperator.

```
key:value[,key:value[...]]
```

## CSV Like Notation
The first value doesn't contain a : therefore values

value[,value[...]]

## Built in types

```
- string str `string 0..255`
- integer int `integer` /(\+|-)?([0-9]+/
- number num `number` /(+|-)?([0-9]+(.[0-9]+))/
- boolean bool `boolean` /(true|false|0|1)/
- datetime `datetime` /(\d{4})(-|/)(\d{2})(-|/)(\d{2}) (\d{2}):(\d{2}):(\d{2})\
- date `date` \(\d{4})(-|/)(\d{2})(-|/)(\d{2})/
- timestamp stamp `timestamp` /(\d{4})(-|/)(\d{2})(-|/)(\d{2}) (\d{2}):(\d{2}):(\d{2}).(\d{9})/
- base64 b64 `base64 0..4096` /[^-A-Za-z0-9+/=]|=[^=]|={3,}$/
- base62 b62 `base62 0..4096` /^[a-zA-Z0-9]+$/
- base16 b16 `base16` /^[a-fA-F0-9]+$/
- email `email` /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
- url `url 0..2048` /@^(https?|ftp)://[^\s/$.?#].[^\s]*$@iS/
- phone `phone 0..22` /^[0-9+\(\)#\.\s\/ext-]+$/
```

[stephenhay url regex](https://mathiasbynens.be/demo/url-regex)

## Examples
### Phone book
```

# Phone
Phone numbers
