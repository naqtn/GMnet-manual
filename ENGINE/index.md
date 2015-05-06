##Welcome to the manual!

Below you will find all pages of this manual. If you are new, start with the tutorial.

Some sections may have a **PLUS** prefix. This means that you need either the *PLUS* version of *HTME* or the classic version of *HTME* and *udphp (Multiplayer without open ports)* installed. If you purchased the classic version, you can buy *udphp* seperately at the Marketplace.

###Tutorial / Getting Started

This tutorial will guide you through the creation of the platformer that comes with the engine and teaches you how to use the engine.
0. [What is HTME?](./tutorial/0_whatishtme)
1. [Basic configuration](./tutorial/1_config)
2. [**PLUS** - Setup udphp](./tutorial/2_udphp1)
3. [**PLUS** - Hosting a mediation server](./tutorial/3_udphp2)
4. [Starting the engine](./tutorial/4_starting)
5. [Setting up the basic platformer](./tutorial/5_platformer)
6. [The network controller](./tutorial/6_networkcontroller)
7. [Adding a player](./tutorial/7_player)
8. [A second room and doors](./tutorial/8_doors)
9. [Making an overlay that shows the name of connected players](./tutorial/9_playerlist)
10. [Adding day/night](./tutorial/10_time)
11. [Creating a chat system](./tutorial/11_chat)
12. [Conclusion / What's next](./tutorial/12_end)
13. [**PLUS** -  Bonus 1 - ONLINE lobby](./tutorial/13_lobby)
14. [Bonus 2 - Global Sync (Sync a pool of variables editable by all)](./tutorial/14_globalsync)
15. [Bonus 3 - LAN lobby](./tutorial/15_lanlobby)
16. [Bonus 4 - Event Handlers for Connecting/Disconnecting](./tutorial/16_disconnect)
16. [Bonus 5 - RPC](./tutorial/17_rpc)

###Important Concepts

* [Local and remote Instances](./concepts/instances)
* [Instance scope and rooms](./concepts/scope)
* [Players and Playerhashes](./concepts/playerhashes)
* [States of the engine](./concepts/states)
* [Variable Groups](./concepts/vargroups)
* [mp_map_syncIn and mp_map_syncOut](./concepts/instancevars)
* [VarGroup SyncTypes (mp_type)](./concepts/synctypes)
* [Tolerance](./concepts/tolerance)
* [Buffer types](./concepts/buffer)
* [CHAT Interface](./concepts/chat)
* [**PLUS** - udphp](./concepts/udphp)
* [**PLUS** - Mediation server](./concepts/mediation)
* [Signed packets](./concepts/signedpackets)
* [The debug overlay](./concepts/debugoverlay)
* [**PLUS** - HTMT The Mediation server debugger](./concepts/htmt)

###Basic Function Reference

#### Sync Functions (mp_*)
* [mp_sync](./functions/sync/mp_sync)
* [mp_unsync](./functions/sync/mp_unsync)
* [mp_stayAlive](./functions/sync/mp_stayAlive)
* [mp_add](./functions/sync/mp_add)
* [mp_addPosition](./functions/sync/mp_addPosition)
* [mp_addBuiltinBasic](./functions/sync/mp_addBuiltinBasic)
* [mp_addBuiltinPhysics](./functions/sync/mp_addBuiltinPhysics)
* [mp_setType](./functions/sync/mp_setType)
* [mp_tolerance](./functions/sync/mp_tolerance)
* [mp_map_syncIn](./functions/sync/mp_map_syncIn)
* [mp_map_syncOut](./functions/sync/mp_map_SyncOut)

#### Tools
* [htme_isLocal](./functions/tools/htme_isLocal)
* [htme_clientIsConnected](./functions/tools/htme_clientIsConnected)
* [htme_clientConnectionFailed](./functions/tools/htme_clientConnectionFailed)
* [htme_isStarted](./functions/tools/htme_isStarted)
* [htme_isServer](./functions/tools/htme_isServer)
* [htme_getPlayers](./functions/tools/htme_getPlayers)
* [htme_findPlayerInstance](./functions/tools/htme_findPlayerInstance)
* [htme_getPlayerNumber](./functions/tools/htme_getPlayerNumber)
* [htme_clientDisconnect](./functions/tools/htme_clientDisconnect)
* [htme_serverDisconnect](./functions/tools/htme_serverDisconnect)
* [htme_serverShutdown](./functions/tools/htme_serverShutdown)

#### CHAT Interface
* [mp_syncAsChatHandler](./functions/chat/mp_syncAsChatHandler)
* [mp_chatGetQueue](./functions/chat/mp_chatGetQueue)
* [mp_chatSend](./functions/chat/mp_chatSend)
* [htme_chatGetMessage](./functions/chat/htme_chatGetMessage)
* [htme_chatGetSender](./functions/chat/htme_chatGetSender)

#### Online Lobby
* [udphp_downloadServerList](./functions/lobby/udphp_downloadServerList)

#### LAN Lobby
* [htme_startLANsearch](./functions/lanlobby/htme_startLANsearch)
* htme_stopLANsearch

#### Global Sync
* [htme_globalGet](./functions/globalsync/htme_globalGet)
* [htme_globalSet](./functions/globalsync/htme_globalSet)
* [htme_globalSetFAST](./functions/globalsync/htme_globalSetFAST)

#### Event handlers
* [htme_serverEventHandlerConnecting](./functions/events/htme_serverEventHandlerConnecting)
* [htme_serverEventHandlerDisconnecting](./functions/events/htme_serverEventHandlerDisconnecting)

#### Configuration
* [htme_init](./functions/config/htme_init)

More documentation may be added later. You can find a documentation of every script in the header of the script files.

###FAQ and More

* [Extending the Engine / Advanced Use](./more/extending)
* [How to update](./more/update)

More will be added to this section later.

###Support

**Please use the [forums](../forum) for support. We will answer there.**
