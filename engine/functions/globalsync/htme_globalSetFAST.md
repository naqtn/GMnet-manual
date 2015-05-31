``htme_globalSetFAST(name,value,datatype)``
--------------

###Description
See [htme_globalSet](functions/globalsync/htme_globalSet).

The only difference is that this script uses the [FAST sync type](concepts/synctypes). This means in rare cases when using this function the global Sync cache may be desynced, therefor only use this function in very specific cases.

More information: [Bonus 2 - Global Sync (Sync a pool of variables editable by all)](tutorial/14_globalsync)

###Example

```javascript
var value = 1+1;
htme_globalSetFAST("name",value,buffer_u8);
```

###Arguments
Name | type | description
---- | ---- | -----------
name | string | The name of the variable
value | real/string | The (new) value of the variable you want to store
datatype | real | See [Buffer type](concepts/buffer)

###Returns
Nothing
