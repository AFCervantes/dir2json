# dir2json
A PHP CLI script to ouput the contents of a whole directory tree to a JSON object

by Ryan, 2015
URL: http://www.ryadel.com/

# What does it do
It turns a directory tree structure like this:

```
/images/
    /gif/
        man.gif
        woman.gif
    /jpg/
        photo1.jpg
        photo2.jpg
    /png/
        avatar.png
    howto.txt,
    readme.md
```

into a JSON object like this:

```
{
    "gif": [
      "man.gif",
      "woman.gif",
      ],
    "jpg": [
      "photo1.jpg",
      "photo2.jpg",
      ],
    "png": [
      "avatar.png"
      ],
    "0": "howto.txt",
    "1": "readme.md"
}
```

It can be very useful when working with Javascript frameworks and/or similar scenarios where you need to load/browse/show a directory structure without being allowed to access the system IO.

The code it's meant to be used as a dedicated CLI script, but you can also execute it from a standard, web-hosted PHP page by populating the $argv[] array directly from code.

# Usage (from CLI)
```
 > php dir2json <targetFolder> <outputFile> [JSON_OPTIONS]
```

JSON_OPTIONS is a bitmask consisting of:
```
  JSON_HEX_QUOT, JSON_HEX_TAG, JSON_HEX_AMP, JSON_HEX_APOS, JSON_NUMERIC_CHECK, 
  JSON_PRETTY_PRINT, JSON_UNESCAPED_SLASHES, JSON_FORCE_OBJECT, JSON_PRESERVE_ZERO_FRACTION, 
  JSON_UNESCAPED_UNICODE, JSON_PARTIAL_OUTPUT_ON_ERROR
```

The behaviour of these constants is described on the JSON constants page:
http://php.net/manual/en/json.constants.php

## Example
```
 > php dir2json ./images out.json JSON_PRETTY_PRINT
```

The json conversion is handled by the native php `json_encode` function (available in PHP 5 >= 5.2.0, PECL json >= 1.2.0, PHP 7). For further info on PHP's json_encode function, read here:
http://php.net/manual/en/function.json-encode.php

