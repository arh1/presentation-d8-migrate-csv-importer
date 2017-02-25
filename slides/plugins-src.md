### Custom Source Plugin

* my_module/src/Plugin/migrate/source/my_plugin.php
* Extend CSV source plugin class
* Plugin discoverability: annotation

~Notes:

* Manipulate source data globally across migrations
* CSV class extends SourcePluginBase class
* We can in turn extend CSV class
* Note plugin's filepath
