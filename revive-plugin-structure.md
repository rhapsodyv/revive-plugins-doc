All revive plugins must follow some folder namming and structure. The plugins must define themself by some XMLs.

# Folder Structure

The plugin must be zipped with the following folder structure:

```Shell
 plugins/etc/___MY_PLUGIN_NAME___.XML
 plugins/etc/___MY_PLUGIN_NAME___.readme.txt
 plugins/etc/___MY_PLUGIN_NAME___.uninstall.txt
 plugins/etc/___MY_PLUGIN_COMPONENT_1_NAME___/___MY_PLUGIN_COMPONENT_1_NAME___.XML

 plugins/___COMPONENT_1___/___MY_PLUGIN_COMPONENT_1_NAME___/___MY_FILES_1___
 plugins/___COMPONENT_2___/___MY_PLUGIN_COMPONENT_2_NAME___/___MY_FILES_2___
 plugins/___COMPONENT_3___/___MY_PLUGIN_COMPONENT_3_NAME___/___MY_FILES_3___
 plugins/___COMPONENT_4___/___MY_PLUGIN_COMPONENT_4_NAME___/___MY_FILES_4___
```

Example:

```
Archive:  helloWorld.zip
  Length     Date   Time    Name
 --------    ----   ----    ----
        0  12-09-14 16:48   plugins/
        0  12-09-14 16:49   plugins/api/
        0  12-09-14 18:45   plugins/api/helloWorld/
     4383  12-09-14 18:45   plugins/api/helloWorld/helloWorld.class.php
        0  12-09-14 17:11   plugins/etc/
        0  12-09-14 17:11   plugins/etc/helloWorld/
      724  12-09-14 17:11   plugins/etc/helloWorld/helloWorld.xml
      683  12-09-14 17:11   plugins/etc/helloWorld.xml
      683  12-09-14 17:11   plugins/etc/helloWorld.readme.txt
      683  12-09-14 17:11   plugins/etc/helloWorld.uninstall.txt
 --------                   -------
     5790                   10 files
```

# Definition Files

## Plugin Definition

The first file describe the plugin itself. Must have the basic info and all the groups that this plugin contain.
A plugin can contain any number of groups. Each group is the part of the plugin that extends some funcionality. For example, some plugin can contain 2 groups: one that extends API funcionality and other that extends REPORT funcionality.

XML example:

```XML
<?xml version="1.0" encoding="ISO-8859-1" ?>
<?xml-stylesheet type="text/xsl" href=""?>

<plugin>
    <name>helloWorld</name>
    <displayName>Hello World Plugin</displayName>
    <creationDate>2014-12-09</creationDate>
    <author>Victor M. Oliveira</author>
    <authorEmail>revive@victormo.com.br</authorEmail>
    <authorUrl>http://www.victormo.com.br</authorUrl>
    <license>GNU Gneral Public License v2</license>
    <description>Plugin that provides basic hello world.</description>
    <version>1.0.1</version>
    <type>package</type>

    <install>
        <files>
            <file path="{PLUGINPATH}">helloWorld.readme.txt</file>
            <file path="{PLUGINPATH}">helloWorld.uninstall.txt</file>
        </files>
        <contents>
            <group name="helloWorld">1</group>
        </contents>
    </install>
</plugin>
```

### XML Fields

* name: Id/Name of the plugin
* displayName
* author
* authorEmail
* authorUrl
* license
* description
* version: version of this plugin
* type: Type of the plugin. For this XML is always *package*
* install: Describes the groups this plugins have. All plugins must have at least on group, because the plugin must have at least one funcinality.
* files: List files for this plugin.
* file: it is a plugin definition file 
* contents: List the groups, where *name* is the name/id of the group (same name of the folder of the group) and the number inside this tag is the install order.

#### ___MY_PLUGIN_NAME___.readme.txt
It is an optional file for you describe with more details this plugin. For example, some notes about exception, change log
and etc.

#### ___MY_PLUGIN_NAME___.uninstall.txt
It is an optional file  that you can show an alert if this plugin is deleted.

## Plugin Group Definition

Each group must have a definition XML.

Example:

```XML
<?xml version="1.0" encoding="ISO-8859-1" ?>
<?xml-stylesheet type="text/xsl" href=""?>

<plugin>
    <name>helloWorld</name>
    <displayName>Hello World Plugin</displayName>
    <creationDate>2014-12-09</creationDate>
    <author>Victor M. Oliveira</author>
    <authorEmail>revive@victormo.com.br</authorEmail>
    <authorUrl>http://www.victormo.com.br</authorUrl>
    <license>GNU Gneral Public License v2</license>
    <description>Plugin that provides basic hello world.</description>
    <version>1.0.1</version>
    <oxversion>2.8.2-rc9</oxversion>
    <extends>api</extends>

    <install>
        <files>
          <file path="{MODULEPATH}api/helloWorld/">helloWorld.class.php</file>
        </files>
        <!-- optional configuration settings -->
        <configuration>
            <!-- only administrator has permissions to change settings in config file -->
            <setting key="keyApiOne" type="text" label="label for key api one" required="0" size="64" visible="1">Defaulf value</setting> 
            <setting key="keyApiTwo" type="text" label="this label is hidden" required="1" size="64" visible="0">hidden</setting>  
            <setting key="keyApiThree" type="checkbox" label="keyApiThree" required="1" size="64" visible="1">false</setting>     
        </configuration>
    </install>
</plugin>
```

### XML Fields

* name: Id/Name of the group
* displayName
* author
* authorEmail
* authorUrl
* license
* description
* version: Version of this group
* oxversion: Revive version required by this plugin to run
* extends: The revive Component this plugin extends. See [Revive Components](#revive-components) to a list of Revive Components.
* install: 
* files: List the files this group have.
* file: Each file must be follow the folder structure as defined above.
* configuration: is an optional configuration settings, you can group all settings key
* setting : is an element into  configuration tag.

### How use settings declared into Plugin Group Definition Xml
You can use optional configuration settings and preferences. Settings are written to a group section. In this case for [helloWorld].
If you want to show this element use visible="1" otherwise set value to "0".
If you want show as required field use required= "1" otherwise set value to "0".
If you want a key type text, use type="text".
If you need a key type checkbox like a boolean var, use type="checkbox".

In above example we have three keys: keyApiOne and keyApiTwo. These are stored in $conf variable, that you can acess from any php file into your plugin. Look this code:

```PHP
$conf = $GLOBALS['_MAX']['CONF']; 
$aHelloWorldConf = $conf['helloWorld']; // this parameter must be the same name of your group that you have defined your keys
$keyApiOne = $aHelloWorldConf['keyApiOne']; // this parameter is the same name key
$keyApiTwo = $aHelloWorldConf['keyApiTwo'];
$keyApiThree = $aHelloWorldConf['keyApiThree'];
```

# Using openXDeveloperToolbox
It is a tool that you can creat in few steps a basic structure for your plugin.
To add this feature for your adserver, download from [repository](https://github.com/revive-adserver/revive-adserver.git). Now you have all files to work on dev mode. Follow steps to install revive.

```
$ cd plugins_repo/
$ ls -l
```
Into this folder you have zipkg.sh for zip any plugin. To use zipkg on your terminal 

```
$ ./zipkg.sh openXDeveloperToolbox
```
Now you will have a new zip openXDeveloperToolbox.zip. Log in with your adm account. So you will see Developer tab.

# Revive Components

* [3rdPartyServers](): TODO
* [admin](): TODO
* [api](components/api-component.md): Extends XMLRPC api
* [authentication](): TODO
* [bannerTypeHtml](): TODO
* [bannerTypeText](): TODO
* [deliveryAdSelect](): TODO
* [deliveryCacheStore](): TODO
* [deliveryLimitations](): TODO
* [deliveryLog](): TODO
* [geoTargeting](): TODO
* [invocationTags](): TODO
* [reports](): To create new Reports (TODO)
* Other class to extend: TODO

All the base classes for plugins are found in the folder *lib/OX/Extension*

# Tutorials
* [Creating an Hello World Api Plugin] (tutorial/api-hello-world.md)
