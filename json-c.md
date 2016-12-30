# `json-c`

## Installation

**Install Binary**
```
$ sudo apt-get install libjson0 libjson0-dev

# If you want to debug your programs and see the various steps for debugging
$ sudo apt-get install libjson0-dbg
```

> https://linuxprograms.wordpress.com/2010/05/20/install-json-c-in-linux/

**Install from Source**

```
$ git clone https://github.com/json-c/json-c.git
$ cd json-c
$ sh autogen.sh

$ ./configure
$ make
$ make install
```

> https://github.com/json-c/json-c

## Compile


```c
// test.c

#include <stdio.h>
#include <stdlib.h>
#include <stddef.h>
#include <string.h>

#include <json/json.h>


int main(int argc, char **argv)
{
	json_object *new_obj;

	MC_SET_DEBUG(1);

    /*
     * {
     *     "glossary": {
     *         "title": "example glossary",
     *         "GlossDiv": {
     *             "title": "S",
     *             "GlossList": [ {
     *                 "ID": "SGML",
     *                 "SortAs": "SGML",
     *                 "GlossTerm": "Standard Generalized Markup Language",
     *                 "Acronym": "SGML",
     *                 "Abbrev": "ISO 8879:1986",
     *                 "GlossDef": "A meta-markup language, used to create markup languages such as DocBook.",
     *                 "GlossSeeAlso": [ "GML", "XML", "markup" ]
     *             } ]
     *         }
     *     }
     * }
    */

	new_obj = json_tokener_parse("/* more difficult test case */"
				     "{ \"glossary\": { \"title\": \"example glossary\", \"GlossDiv\": { \"title\": \"S\", \"GlossList\": [ { \"ID\": \"SGML\", \"SortAs\": \"SGML\", \"GlossTerm\": \"Standard Generalized Markup Language\", \"Acronym\": \"SGML\", \"Abbrev\": \"ISO 8879:1986\", \"GlossDef\": \"A meta-markup language, used to create markup languages such as DocBook.\", \"GlossSeeAlso\": [\"GML\", \"XML\", \"markup\"] } ] } } }");
	printf("new_obj.to_string()=%s\n", json_object_to_json_string(new_obj));
	json_object_put(new_obj);

	return EXIT_SUCCESS;
}
```

Compile using cmd:

```shell
$ gcc test.c -ljson -o test
```

## Reference

- https://linuxprograms.wordpress.com/2010/05/20/json-c-libjson-tutorial/
- https://github.com/json-c/json-c/wiki
