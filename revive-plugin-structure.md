All revive plugins must follow some folder namming and structure. The plugins must define themself by some XMLs.

# Folder Structure

The plugin must be zipped with the following folder structure:

```Shell
 plugins/etc/___MY_PLUGIN_NAME___.XML
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
 --------                   -------
     5790                   9 files
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
* contents: List the groups, where *name* is the name/id of the group (same name of the folder of the group) and the number inside this tag is the install order.

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


# Revive Components

* [3rdPartyServers](): TODO
* [admin](): TODO
* [api](api-component.md): Extends XMLRPC api
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
