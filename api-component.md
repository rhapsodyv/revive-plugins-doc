To enhance Revive XMLRPC Api, you must build a plugin with a group that extends api component.

# How API Plugins Works 

Every api plugin is called by **www/api/v2/xmlrpc/index.php**:
```php
// Merge the plugins' dispatch maps with core.
// Function names should be namespaced.
$aComponents = OX_Component::getComponents('api');
$aMaps = OX_Component::callOnComponents($aComponents, 'getDispatchMap');
foreach($aMaps as $map) {
    $dispatches = array_merge($dispatches, $map);
}
```

So, it's clear how to build an api plugin now. We just need to extend **Plugins_Api** (*lib/OX/Extension/api/Api.php*) class and implement **getDispatchMap** returning our methods map, like the ones found in the begging of **www/api/v2/xmlrpc/index.php**.

### XMLRPC Api Definition Example:

Added comments in line.
```php
$dispatches = array(
    // Logon
   'ox.logon' => array(                             /* Method NAME */
        'function'  => array($fc, 'logon'),         /* Callback */
        'signature' => array(
            array('string', 'string', 'string')     /* definition ==> 1.Return Type, 2.First Param, 3.Second Param,.... */
        ),
        'docstring' => 'Logon method'               /* method docs */
    ),
```
