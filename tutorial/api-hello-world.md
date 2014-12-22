# Hello World API Plugin

In this tutorial we will creating a simple plugin that extends XMLRPC funcionality and add a new API call, *xx.helloWorld*.

## 1. Creating Folder Structure

The very first thing to do is create the folder structure to work on.

* Project Folder

First we need a project folder:
```Shell
$ mkdir api-hello-world
```
* Plugin Root Folder

The very first folder inside our plugin, must be **plugins**:
```Shell
$ cd api-hello-world
$ mkdir plugins
```

* Basic Plugins Folders

Now we must have a folder for the XMLs definitions called **etc**, and a folder for each group we will create. We are creating just one group called **helloWorld**:
```Shell
$ cd plugins
$ mkdir etc
$ mkdir etc/helloWorld
```

* Plugin Group Folders

Now we need the folder where we going to put our code. The parent folders must be named with component each group will extend. Because we are creating just an API group, we need an **api** folder as parent of our **helloWorld** group:
```Shell
$ cd plugins
$ mkdir api
$ mkdir api/helloWorld
```

## 2. Creating Plugin Definition XML

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
    <version>1.0.0</version>
    <type>package</type>

    <install>
        <contents>
            <group name="helloWorld">1</group>
        </contents>
    </install>
</plugin>
```

## 3. Creating Our Plugin API Class

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
    <version>1.0.0</version>
    <oxversion>2.8.2-rc9</oxversion>
    <extends>api</extends>

    <install>
        <files>
          <file path="{MODULEPATH}api/helloWorld/">helloWorld.class.php</file>
        </files>
    </install>
</plugin>
```

## 3. Creating Our Plugin API Class

The class file must be inside the group folder, as defined in the group XML above:

> plugins/api/helloWorld/helloWorld.class.php

Our class must follow PHP old namespaces naming covention - following the folder strucuture until the class file:

> Plugins_Api_HelloWorld_helloWorld

### Our Method definition

```php
  function getDispatchMap()
  {
    return array(
     'xx.helloWorld' => array(                          /* xx.helloWorld method */
          'function'  => array($this, 'helloWorld'),    /* the callback is a method called helloWorld in this class */
          'signature' => array(
              array('string')                           /* we just will return a string */
          ),
          'docstring' => 'Hello World method'
        ),
      );
  }
```

### Coding the Callbacks

```php
  function helloWorld()
  {
    return XmlRpcUtils::stringTypeResponse("Hello World");
  }
```

### Final Class

```php
class Plugins_Api_HelloWorld_helloWorld extends Plugins_Api
{
  function getDispatchMap()
  {
    return array(
     'xx.helloWorld' => array(
          'function'  => array($this, 'helloWorld'),
          'signature' => array(
              array('string')
          ),
          'docstring' => 'Hello World method'
        ),
      );
  }

  function helloWorld()
  {
    return XmlRpcUtils::stringTypeResponse("Hello World");
  }
}
```

## 4. Packaging the Plugin

To pack our plugin, we just need zip the contents:

```Shell
$ cd api-hello-world
$ zip -r helloWorld.zip plugins
```

The contents of the zip must be the following:
```Shell
$ cd api-hello-world
$ unzip -l helloWorld.zip

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
     5790                   8 files

```

## 5. Uploading to Revive

## 6. Testing Our XMLRPC Method
