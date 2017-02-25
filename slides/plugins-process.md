### Custom Process Plugins

* my_module/src/Plugin/migrate/process/MyPlugin.php
* Extend ProcessPluginBase class
* Just need one method: transform
* Plugin discoverability: annotation

~Notes:

* Custom per-field transformations b/w source and dest
* Note plugin's filepath
