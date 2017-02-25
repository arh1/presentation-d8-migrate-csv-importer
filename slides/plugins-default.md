### Core/Contrib Plugins

* Lots out of the box
* <em>default_value</em>, _concat_, <em>machine_name</em>, _callback_, ...
* Some contrib module plugins
* _console plugin:debug migrate.[process|source|destination]_

~Notes:

* Only need to supply config/yml
* Source: e.g. d6_node (not too many by def)
* Destination: any entity type, config, url aliases
* Lots of default process plugins
* callback process plugin: simple processing (any PHP function w/ source val as single arg)
* Note "default" syntax is shorthand for "get"/default plugin
* Console to list available plugins
