``mp_addBuiltinBasic(groupname,interval)``
--------------

###Description
Adds a new group of variables to be synced to this instance.

The variables are:
* image_alpha,image_angle,image_blend,image_index,image_speed, image_xscale,image_yscale,visible

###Example

```gml
///Create Event
mp_sync();
mp_addBuiltinBasic("drawing",10*room_speed);;
```

###Arguments
Name | type | description
---- | ---- | -----------
groupname | string | The name of the group, this is only used locally to identify this group, for example if you want to use [mp_setType](functions/sync/mp_setType)
interval | real | The interval in which the variable group get's synced with the other players

###Returns
Nothing