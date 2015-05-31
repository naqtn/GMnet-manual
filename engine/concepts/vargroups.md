Variable Groups
--------------

**Variable Groups** or **VarGroups** describe a group of variables of an instance that are synced via the engine.

###Create a new VarGroup:
* [**mp_add**(groupname,variables,datatype,interval);](functions/sync/mp_add)
* [**mp_addPosition**(groupname,interval);](functions/sync/mp_addPosition)
* [**mp_addBuiltinBasic**(groupname,interval);](functions/sync/mp_addBuiltinBasic)
* [**mp_addBuiltinPhysics**(groupname,interval);](functions/sync/mp_addBuiltinPhysics)

###Change the [SyncType](concepts/synctypes) of the group:
* [**mp_setType**(groupname,syncType);](functions/sync/mp_setType)

###Give the group a [Tolerance](concepts/tolerance):
* [**mp_tolerance**(groupname,tolerance);](functions/sync/mp_tolerance)