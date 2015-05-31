##CHAT Interface

The CHAT (Custom Handler for Advanced Traffic) Interface is a new way of syncing information between players.

Instead of using objects and instances, this uses a more classic approach. Using the CHAT Interface you can send and retrieve string messages, with the support for multiple channel.

CHAT messages are sent using the **IMPORTANT** [sync type](concepts/synctypes).

###Tutorial
* [Creating a chat system with it](tutorial/11_chat)
* [Call scripts over the network using the CHAT Interface (RPC)](tutorial/17_rpc)

###Commands
* [mp_syncAsChatHandler](./functions/chat/mp_syncAsChatHandler) for registering an object to recieve and send messages on a channel.
* [mp_chatGetQueue](./functions/chat/mp_chatGetQueue) to recieve new messages.
* [mp_chatSend](./functions/chat/mp_chatSend) to send messages.
* [htme_chatGetMessage](./functions/chat/htme_chatGetMessage) to get the message out of a message.
* [htme_chatGetSender](./functions/chat/htme_chatGetSender) to get the author of a message.