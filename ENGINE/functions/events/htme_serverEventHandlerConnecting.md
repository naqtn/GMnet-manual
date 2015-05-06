``htme_serverEventHandlerConnecting(script)``
--------------

###Description
Call a script if a new player connected. This script has to meet the following
specifications:

#### Callback Arguments:      
Name | type | description
---- | ---- | -----------
player_map | ds_map | a ds_map with the keys ip and port, which contain ip and port of the player
        
#### Callback Returns:
TRUE if the connection is accepted. The engine will then register the player  
FALSE if the connection should be refused, the server will abort connection

###Example
See [BONUS 4 - Event Handlers for Connecting/Disconnecting ](tutorial/16_events).


###Arguments
Name | type | description
---- | ---- | -----------
script | ressource id of a script | The script to call when a player connected.

###Returns
Nothing
