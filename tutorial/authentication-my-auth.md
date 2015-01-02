#My Auth Plugin

This little guide will not make the complex Authentication Plugin, but it will give you an introduction to writing one.

## 1. Creating Folder Structure

The very first thing to do is create the folder structure to work on.

### Project Folder

First we need a project folder:
```Shell
$ mkdir myAuth
```

###Plugin Root Folder

The very first folder inside our plugin, must be **plugins**:
```Shell
$ cd myAuth
$ mkdir plugins
```

###Basic Plugins Folders

Now we must have a folder for the XMLs definitions called **etc**, and a folder for each group we will create. We are creating just one group called **auth**:
```Shell
$ cd plugins
$ mkdir etc
$ mkdir etc/auth
```

###Plugin Group Folders

Now we need the folder where we going to put our code. The parent folders must be named with component each group will extend. Because we are creating just an Authentication group, we need an **authentication** folder as parent of our **auth** group:
```Shell
$ cd plugins
$ mkdir authentication
$ mkdir authentication/auth
```

## 2. Creating Plugin Definition XML
Copy code below and save as myAuth/plugins/etc/**myAuth.xml**

```XML
<?xml version="1.0" encoding="ISO-8859-1" ?>
<?xml-stylesheet type="text/xsl" href=""?>

<plugin>
    <name>myAuth</name>
    <displayName>My Authentication Plugin</displayName>
    <creationDate>2015-01-02</creationDate>
    <author>Karen Mikaeka Saavedra Chavez</author>
    <authorEmail>karen.mikaela@gmail.com</authorEmail>
    <authorUrl>http://www.karen.mikaela</authorUrl>
    <license>GNU Gneral Public License v2</license>
    <description>Plugin that provides basic authentication.</description>
    <version>1.0.0</version>
    <type>package</type>
    <install>
        <contents>
            <group name="auth">0</group>
        </contents>
    </install>
</plugin>
```

## 3. Creating Group Definition
Copy code below and save as myAuth/plugins/etc/auth/**auth.xml**

```XML
<?xml version="1.0" encoding="ISO-8859-1" ?>
<?xml-stylesheet type="text/xsl" href=""?>

<plugin>
    <name>auth</name>
    <displayName>My Auth Plugin</displayName>
    <creationDate>2015-01-02</creationDate>
    <author>Karen Mikaeka Saavedra Chavez</author>
    <authorEmail>karen.mikaela@gmail.com</authorEmail>
    <authorUrl>http://www.karen.mikaela</authorUrl>
    <license>GNU Gneral Public License v2</license>
    <description>Plugin that provides basic authentication.</description>
    <version>1.0.0</version>
    <oxversion>3.1.0</oxversion>
    <extends>authentication</extends>
    <install>
        <files>
            <file path="{MODULEPATH}authentication/auth/">authComponent.class.php</file>
        </files>
    </install>
</plugin>
```

## 4. Creating Our authComponent main Class

The class file must be inside the group folder, as defined in the group XML above:

> plugins/authentication/auth/authComponent.class.php

Our class must follow PHP old namespaces naming covention - following the folder strucuture until the class file:

> Plugins_Authentication_Auth_AuthComponent

### Extends from Plugins_Authentication

```php
/* 
 * Import extension authentication.php
 */
require_once LIB_PATH . '/Extension/authentication/authentication.php';

class Plugins_Authentication_Auth_AuthComponent extends Plugins_Authentication{
    var $allowUsers = array("admin");
}
```

### Overwrite checkPassword method
In this example we will only accept the user login is your username is in array **$allowUsers**

```php
function checkPassword($username, $password){
    if(in_array(strtolower($username),$this->allowUsers)){
        return parent::checkPassword($username, $password);
    }else{
        return false;
    }
}  
```

### Final Class
Copy code below and save as plugins/authentication/auth/**authComponent.class.php**

```php
<?php

/* 
 * Import extension authentication.php
 */
require_once LIB_PATH . '/Extension/authentication/authentication.php';

class Plugins_Authentication_Auth_AuthComponent extends Plugins_Authentication{
    var $allowUsers = array("adm");

    function checkPassword($username, $password){
        if(in_array(strtolower($username),$this->allowUsers)){
            return parent::checkPassword($username, $password);
        }else{
            return false;
        }
    }
}
?>
```
## 5. Add readme  and uninstall file
In this section you can put your consideration when you are installing or if you want delete the plugin.

Create two txt files:
* First file save as myAuth/plugins/etc/**myAuth.readme.txt**
* Second file save as myAuth/plugins/etc/**myAuth.uninstall.txt**

Now edit **auth.xml** file, and add the reference in **install** tag

```XML
<files>
    <file path="{PLUGINPATH}">myAuth.readme.txt</file>
    <file path="{PLUGINPATH}">myAuth.uninstall.txt</file>
</files>
```
## 6. Packaging the Plugin

To pack our plugin, we just need zip the contents:

```Shell
$ cd myAuth
$ zip -r myAuth.zip plugins
```

The contents of the zip must be the following:
```sh
$ cd myAuth
$ unzip -l myAuth.zip

Archive:  myAuth.zip
└── plugins
    ├── authentication
    │   └── auth
    │       └── authComponent.class.php
    └── etc
        ├── auth
        │   └── auth.xml
        ├── myAuth.readme.txt
        ├── myAuth.uninstall.txt
        └── myAuth.xml

```

## 7. Uploading to Revive
Go to plugins section and upload the .zip
Edit **$REVIVE_PATH/var/MY_HOST.conf.php**
Set the property type
```
[authentication]
type="authentication:auth:authComponent"
```
