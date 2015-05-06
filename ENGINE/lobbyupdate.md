The lobby update for HTME PLUS and UDPHP
--------------

**Version 1.1.3** of UDPHP and **Version 1 of HTME** introduce a new lobby. This whole update is quite huge. If you experience problems, please  tell me!

You will find everything about it that you need to know in the new chapter of the tutorial, or if you are a UDPHP user, check out the new ``lobby.html`` included with the demo project.

For HTME users this update also includes a way of identifying players using numbers (Player 1, Player 2 etc.). You can find new manual pages for this under the *Basic Function Reference*.

**For both projects: Please make sure to create a new project when you want to test out the demo project, do not update your old demo project. Starting fresh is easier**.

Also, as HTME user, check out part 1 of the manual again, the section ***Adding the engine to a project***, because some things changed for people that use HTME and UDPHP as seperate assets.

**You need to update the mediation/master server!**

###Changelog for UDPHP Master Server

* (**Has to be updated!**)
* Command line parameters! Use ``-h`` to see a list of arguments.
* Set the port via a new command line option.
* Log to seperate file and change what's being logged.
* Support for the new lobby system and data strings (lobby can be disabled via command line options).

###Changelog for UDPHP 1.1.3

* Fixed crashes related to clientGetServerIP and clientGetServerPort
* Added functions to download a list of servers from the master server
* Added 8 data strings that can be used to identify a server, they get synced to the master server and can be retrieved by clients and the master server when downloading a list of servers
* (Added lobby to demo project)

####Changed files

```
Objects:
obj_udphphtme_lobby.object.gmx (added)

Rooms:
udphphtme_lobby.room.gmx (added)

Scripts:
udphp_clientGetServerIP.gml
udphp_clientGetServerPort.gml
udphp_clientNetworking.gml
udphp_config.gml
udphp_createServer.gml
udphp_serverNetworking.gml
udphp_serverPunch.gml
udphp_serverSetData.gml (added)
udphp_serverCommitData.gml (added)
udphp_readData.gml (added)
udphp_downloadServerList.gml (added)
udphp_downloadNetworking.gml (added)
udphp_clientReadData.gml (added)
```

###Changelog for HTME 1.0

* **PLUS** - Fixed a bug when connecting via udphp, where the server port would not update correctly when corrected by the master server
* Added a new string to identify your game that has to be changed in htme_init (``gamename``)
* **PLUS** - Added functions to manipulate and sync the 8 data strings as introduced in UDPHP 1.1.3 (see changelog of UDPHP)
* **PLUS** - (Added lobby to demo project)
* Also check out the UDPHP changes when using HTME PLUS.
* Added ``htme_getPlayerNumber`` to identify players using integer numbers.

####Changed files

```
Objects:
htme_obj_menu.object.gmx

Scripts:
htme_serverEventPlayerConnected.gml
htme_serverStart.gml
htme_init.gml
htme_step.gml
htme_getPlayerNumber.gml (added)
htme_setGamename.gml (added)
htme_getGamename.gml (added)
htme_setData.gml (added)
htme_getDataServer.gml (added)
htme_commitData.gml (added)
+ all files from UDPHP when using the PLUS version
```