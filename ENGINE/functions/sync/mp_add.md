``mp_add(groupname,variables,datatype,interval)``
--------------

###Description
Adds a new [group of variables](concepts/vargroups) to be synced to this instance.

Please read this manual page when using mp_add: [mp_map_syncIn and mp_map_syncOut](concepts/instancevars)

###Example

```javascript
///Create Event
mp_sync();
mp_add("playerName","name",buffer_string,10*room_speed);;
```

###Arguments
Name | type | description
---- | ---- | -----------
groupname | string | The name of the group, this is only used locally to identify this group, for example if you want to use [mp_setType](functions/sync/mp_setType)
variables | string | A list of local variables of the instance seperated  with commas
datatype | real,buffer_* | A value of a "buffer_" constant to specify the data type of all variables in this group. [See the manual](concepts/buffer) for a list of datatypes and their meanings. All datatypes from enum mp_buffer_types are also allowed but should not be used by you as a user!
interval | real | The interval in which the variable group get's synced with the other players

###Returns
Nothing