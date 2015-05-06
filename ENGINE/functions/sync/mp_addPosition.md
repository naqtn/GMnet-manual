``mp_addPosition(groupname,interval)``
--------------

###Description
Adds a new group of variables to be synced to this instance.

The variables are:
* x,y

###Example

```javascript
///Create Event
mp_sync();
mp_addPosition("pos",10*room_speed);;
```

###Arguments
Name | type | description
---- | ---- | -----------
groupname | string | The name of the group, this is only used locally to identify this group, for example if you want to use [mp_setType](functions/sync/mp_setType)
interval | real | The interval in which the variable group get's synced with the other players

###Returns
Nothing