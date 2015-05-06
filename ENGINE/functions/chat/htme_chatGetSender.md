``htme_chatGetSender(chat_queue_entry)``
--------------

###Description
Get the sender of a CHAT Interface message. See [mp_chatGetQueue](functions/chat/mp_chatGetQueue) for details.

###Example
Read the tutorial [about creating a chat system](tutorial/11_chat) for more information.

###Arguments
Name | type | description
---- | ---- | -----------
chat_queue_entry | string | An entry of the queue returned by [mp_chatGetQueue](functions/chat/mp_chatGetQueue).

###Returns
Playerhash of the player that sent this message
