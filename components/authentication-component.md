You can change the flow that authentication works, to do that you can extend Plugins_Authentication class, it is a parent class for Authentication plugins.

# How Authentication Plugins Works
Plugins_Authentication extends from OX_Component, so you can override some methods like: 
* checkPassword,
* logout,
* displayLogin,
* etc.

You can see all methods and how it is defined accessing **$REVIVE_PATH/var/lib/OX/Extension/authentication/authentication.php**.

Plugins_Authentication is called by Auth.php(**$REVIVE_PATH/lib/OA/Auth.php**) that reads a propriety "type" have defined in **$REVIVE_PATH/var/MY_HOST.conf.php** file. By default this property is setted as internal. So when you are writing a new implementation from Plugins_Authentication you must update in conf file the parameter type.

Original conf:
```
...
[authentication]
type="internal"
...
```
The name of type is a string that follow this rule: extensionName:groupName:componentName.
Example to set a custom type:
```
...
[authentication]
type="authentication:auth:authComponent"
...
```
### Authentication Example:
The pluging should look something like this:

```sh
└── plugins
    ├── authentication
    │   └── auth
    │       ├── authComponent.class.php
    └── etc
        ├── auth
        │   ├── auth.xml
        ├── myAuth.readme.txt
        ├── myAuth.uninstall.txt
        └── myAuth.xml

```

# Tutorial
* [Creating MyAuthentication Plugin](../tutorial/authentication-my-auth.md)
* [A basic example Authentication plugin](https://github.com/karen-mikaela/my-auth-revive)
* [Authentication plugin using Active Directory (Adldap)](https://github.com/karen-mikaela/ldap-auth)
