``mp_tolerance(groupname,tolerance)``
--------------

###Description
More information: [Tolerance](concepts/tolerance).

###Example

```gml
///Create Event
mp_sync();
mp_addPosition("pos",1);
mp_tolerance("pos",10);
```

###Arguments
Name | type | description
---- | ---- | -----------
groupname | string | The name of the group
interval | real | The tolerance to apply

###Returns
Nothing