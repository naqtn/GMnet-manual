Players and Playerhashes
--------------

Players are identified by hash strings.

You can loop through all players using this loop over the list returned by [htme_getPlayers](functions/tools/htme_getPlayers):

```gml
var playerlist = htme_getPlayers();
for(var i = 0;i<ds_list_size(playerlist);i++) {
    var player = ds_list_find_value(playerlist,i);
}
```

``player`` will contain the hash of the player.  
This hash can be used by [htme_findPlayerInstance](functions/tools/htme_findPlayerInstance).