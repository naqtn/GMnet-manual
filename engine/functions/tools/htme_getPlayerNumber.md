``htme_getPlayerNumber(playerhash)``
--------------

###Description
Extracts the number of the player from the playerhash
The number starts at 1 for the server, 2 is the first connected client, 3 the third and so on. 
If 2 disconnects, the next player connecting will occupy place 2 again.

###Arguments
Name | type | description
---- | ---- | -----------
playerhash | string | A playerhash as stored in the list that you can get with htme_getPlayers.

###Returns
The player number