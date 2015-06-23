``mp_setType(group,type)``
--------------

###Description
Changes the type with which a group will be synced to the other clients.

More information: [VarGroup SyncTypes (mp_type)](concepts/synctypes)

###Example

```gml
///Create Event
mp_sync();
mp_addBuiltinPhysics("physics",10*room_speed);
mp_setType("physics",mp_type.SMART);
```

###Arguments
Name | type | description
---- | ---- | -----------
groupname | string | The name of the group of which you want to change the type of
interval | real | The values of the enum mp_type can be seen in htme_init or [the manual](concepts/synctypes).

###Returns
Nothing