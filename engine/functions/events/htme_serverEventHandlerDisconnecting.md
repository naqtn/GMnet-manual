``htme_serverEventHandlerDisconnecting(script)``
--------------

###Description
Call a script if a player disconnected. This script has to meet the following
specifications:

#### Callback Arguments:      
Name | type | description
---- | ---- | -----------
player_map | ds_map | a ds_map with the keys ip and port and hash
        
#### Callback Returns:
Nothing

###Example
See [BONUS 4 - Event Handlers for Connecting/Disconnecting ](tutorial/16_events).


###Arguments
Name | type | description
---- | ---- | -----------
script | ressource id of a script | The script to call when a player disconnected.

###Returns
Nothing
