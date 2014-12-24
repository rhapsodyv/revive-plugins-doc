# How to Uninstall and Cleanup a Plugin Install

A working and correctly installed plugin can be normally uninstalled by the revive admin configuration interface. Just go to *Administrator Account > Plugins* find your plugin and uninstall it.

But when we are developing things never work every time... So follow next...

# How to Uninstall and Cleanup a Broken Plugin

To remove a plugin manually follow this steps:

### 1. Remove the plugin code
```
$ rm -rf $REVIVE_PATH/plugins/COMPONENT_XX/MY_PLUGIN_FOLDER_1
$ rm -rf $REVIVE_PATH/plugins/COMPONENT_YY/MY_PLUGIN_FOLDER_2
```
###2. Remove the plugin config

Edit the file **$REVIVE_PATH/var/MY_HOST.conf.php**, search for **[plugins]** and **[pluginGroupComponents]** and remove references for your plugin.

###3. Remove any other file or table your plugin created
