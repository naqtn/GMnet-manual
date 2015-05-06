``mp_map_syncOut(varName, variable)``
--------------

###Description
More information: [mp_map_syncIn and mp_map_syncOut](concepts/instancevars)

###Arguments
Name | type | description
---- | ---- | -----------
varName | string | Name of the variable to get
variable | any | Value of the variable that the instance currently has. Will later be used to compare them to values in the engine. Currently this is returned if the engine has no valid data for this varName.

###Returns
Value of varName in the variable map of this instance