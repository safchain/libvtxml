libvtxml
========

Very tiny stream-oriented XML parser

Example:

```xml
<root>
	<node1 name="vector" value="35">
		<subnode unique="true"/>
	</node1>
</root>
```


```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "xml.h"

int text(char *text, XML_CONFIG *config) {
	if (strcmp(config->xpath, "/root/node1") == 0) {
		printf ("%s : %d\n", text, config->line);
	}
}

int tag_open (char *tagname, XML_CONFIG *config) {
	if (strcmp(config->xpath, "/root/node1") == 0) {
		printf ("open %s : %d\n", tagname, config->line);
	}
}

int tag_attr(char *tagname, char *attrname, char *attrvalue, XML_CONFIG *config) {
	printf ("%s - %s = %s: %d\n", tagname, attrname, attrvalue, config->line);
}

int tag_close (char *tagname, XML_CONFIG *config) {
	if (strcmp(config->xpath, "/root/node1") == 0) {
		printf ("close %s : %d\n", tagname, config->line);
	}
	else if (strcmp(config->xpath, "/root/node1/subnode") == 0) {

	}

	return 0;
}

int main (int argc, char **argv) {
	XML_CONFIG *xml_config;
	XML_CALLBACKS xc;

        if ((xml_config = xml_alloc_config()) == NULL) {
		return -1;
        }

	memset(&xc, 0, sizeof(xc));

	xc.on_text = text;
	xc.on_tag_attr = tag_attr;
	xc.on_tag_open = tag_open;
	xc.on_tag_close = tag_close;

	xml_add_callback(xml_config, "/root/node1", &xc);

	if (xml_parse_file(argv[1], xml_config) == -1) {
		return -1;
        }

	if (strlen(xml_config->error) != 0) {
                fprintf (stderr, "error: %s", xml_config->error);	
		return -1;
	}

	xml_free_config(xml_config);
}
```
