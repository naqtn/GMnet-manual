Instance scope and rooms
--------------

Non-persistent instances will disappear if they leave the room. It doesn't matter if a [local instance](concepts/instances) or a remote instance leaves the room, it will always disappear.

Persistent instances will follow the local player into the next room. That means persistent remote instance will be destroyed, persistent local instances not.

stayAlive instances (objects where [mp_stayAlive();](functions/sync/mp_stayAlive) was used) that are also persistent will always follow the local player into a new room, no matter if it's a local or remote instance.

Here's a table that illustrates that:

**INSTANCE WAS CREATED BY PLAYER A IN ROOM A**
![Table](images/4.PNG)