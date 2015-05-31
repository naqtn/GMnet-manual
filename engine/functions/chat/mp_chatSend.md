``mp_chatSend(message,[to])``
--------------

###Description
Object has to be set up with [mp_syncAsChatHandler](functions/chat/mp_syncAsChatHandler) first, otherwise an error will occur.

Send message via the CHAT Interface over this chanel.
The message has to be a string. You can also experiment with json to send more
complicated data.

This message will by default be sent to all clients and the server [also the local 
game!] and can be retrieved via [mp_chatGetQueue](functions/chat/mp_chatGetQueue).

Use the additional 'to' argument to only send this message to one player.

###Example
Read the tutorial [about creating a chat system](tutorial/11_chat) for more information.

###Arguments
Name | type | description
---- | ---- | -----------
message | string | The message to send
[to] | string | (optional; Will send to all by default) hash of the player that the message should be sent to.

###Returns
Nothing
