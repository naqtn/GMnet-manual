``mp_chatGetQueue()``
--------------

###Description
Object has to be set up with mp_syncAsChatHandler first, otherwise an error will occur.

Get a ds_queue containing all not processed string that recieved via this channel.
All entries in this queue can be decoded using these commands:
* [htme_chatGetSender](functions/chat/htme_chatGetSender) - To get the playerhash of the player that sent this message
* [htme_chatGetMessage](functions/chat/htme_chatGetMessage) - To get the chat message.

###Example
Read the tutorial [about creating a chat system](tutorial/11_chat) for more information.

###Arguments
None

###Returns
A ds_queue, it's entries can be decoded using the functions above.
