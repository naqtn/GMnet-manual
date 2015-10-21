##GMnet ENGINE マニュアル: インデックス

ようこそ！
いかにこのマニュアルの全てのページが一覧されています。
GMnet ENGINE にはじめてふれるのであれば、チュートリアルから始めてください。

幾つかの節には **PLUS** の表記がついています。
これらのページは GMnet ENGINE を使う場合にのみ関係します。
GMnet CORE を使うか設定で GMnet PUNCH を無効にする場合には、
これらのページは適用されません。
詳しくは[GMnet CORE と ENGINE の違い](./versiondifferences)で確認してください。


**Note:** GMnet ENGINE は以前 "HappyTear Multiplayer Engine"（略称 HTME）と呼ばれていました。
この名前は現在もマニュアルページの幾つかに残っています。
またこの理由で、スクリプトのプレフィックスには HTME が使われています。
GMnet PUNCH は以前 UDPHP と呼ばれていました。これも同様の扱いになっています。


###チュートリアル / はじめに
このチュートリアルは platformer （訳注：ジャンプ・アクション・ゲーム） を作るのを通して、
エンジンの使い方を解説します。

0. （訳済） [What is GMnet ENGINE?](./tutorial/0_whatishtme)
1. （訳済） [Basic configuration](./tutorial/1_config)
2. （訳済） [**PLUS** - Setup GMnet PUNCH](./tutorial/2_udphp1)
3. （訳済） [**PLUS** - Hosting a mediation server](./tutorial/3_udphp2)
4. （訳済） [Starting the engine](./tutorial/4_starting)
5. （訳済） [Setting up the basic platformer](./tutorial/5_platformer)
6. （訳済） [The network controller](./tutorial/6_networkcontroller)
7. （訳済） [Adding a player](./tutorial/7_player)
8. （訳済） [A second room and doors](./tutorial/8_doors)
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
* [**PLUS** - GMnet PUNCH](./concepts/udphp)
* [**PLUS** - Master server (GMnet GATE.PUNCH)](./concepts/mediation)
* [Signed packets](./concepts/signedpackets)
* [The debug overlay](./concepts/debugoverlay)
* [**PLUS** - GMnet GATE.TESTER](./concepts/htmt)

###基本関数リファレンス

#### 同期関数 (mp_*)
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

#### ツール
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

#### チャット・インタフェース
* [mp_syncAsChatHandler](./functions/chat/mp_syncAsChatHandler)
* [mp_chatGetQueue](./functions/chat/mp_chatGetQueue)
* [mp_chatSend](./functions/chat/mp_chatSend)
* [htme_chatGetMessage](./functions/chat/htme_chatGetMessage)
* [htme_chatGetSender](./functions/chat/htme_chatGetSender)

#### オンライン・ロビー
* [udphp_downloadServerList](./functions/lobby/udphp_downloadServerList)

#### LAN ロビー
* [htme_startLANsearch](./functions/lanlobby/htme_startLANsearch)
* htme_stopLANsearch

#### Global Sync
* [htme_globalGet](./functions/globalsync/htme_globalGet)
* [htme_globalSet](./functions/globalsync/htme_globalSet)
* [htme_globalSetFAST](./functions/globalsync/htme_globalSetFAST)

#### イベント・ハンドラー
* [htme_serverEventHandlerConnecting](./functions/events/htme_serverEventHandlerConnecting)
* [htme_serverEventHandlerDisconnecting](./functions/events/htme_serverEventHandlerDisconnecting)

#### 設定
* [htme_init](./functions/config/htme_init)

ドキュメントは今後増えていく予定です。
全てのスクリプトの先頭部分にそのドキュメントが書かれています。

###FAQ and More

* [Extending the Engine / Advanced Use](./more/extending)
* [How to update](./more/update)

この節には後ほど追加があるでしょう。

###Support

**サポート情報は[フォーラム](../../forum)で得られます。質問にはここで回答いたします。**

---
##GMnet ENGINE Manual: Index

Welcome! Below you will find all pages of this manual. If you are new, start with the tutorial.

Some sections may have a **PLUS** prefix. These pages are only relevant if you are using GMnet ENGINE. If you are GMnet CORE or if you disabled GMnet PUNCH in the settings, these pages do not apply for you. For more information, check the page on [differences between GMnet CORE and ENGINE](./versiondifferences)

**Note:** GMnet ENGINE was previously called the "HappyTear Multiplayer Engine" (or HTME for short). This name may be still present on some pages of the manual, also all scripts and files are prefixed with "HTME" for this reason. GMnet PUNCH was previously called UDPHP, the same applies for it.

###Tutorial / Getting Started

This tutorial will guide you through the creation of the platformer that comes with the engine and teaches you how to use the engine.
0. [What is GMnet ENGINE?](./tutorial/0_whatishtme)
1. [Basic configuration](./tutorial/1_config)
2. [**PLUS** - Setup GMnet PUNCH](./tutorial/2_udphp1)
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
* [**PLUS** - GMnet PUNCH](./concepts/udphp)
* [**PLUS** - Master server (GMnet GATE.PUNCH)](./concepts/mediation)
* [Signed packets](./concepts/signedpackets)
* [The debug overlay](./concepts/debugoverlay)
* [**PLUS** - GMnet GATE.TESTER](./concepts/htmt)

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

**Please use the [forums](../../forum) for support. We will answer there.**
