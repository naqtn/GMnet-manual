##3. Server

Okay so we are done in obj_control. Let’s go to **obj_server** and **obj_client**. Both have the same structure.
_GMnet PUNCH_ uses the **create event**, the **step event** and the **networking event** of both. The following scripts can jsut be inserted as [the first] entries in these events. The GMnet PUNCH scripts will only run when needed and they won’t interupt your networking. If they do, please contact the support!

###Server create event

**obj_server’s create event** get’s called on server creation (obviously). You need to create a **player list (ds_list)** there. This list will be used by GMnet PUNCH to store all players in. How to use them in your game will be explained later, but this is your only way to tell which player communicates with the server!
You will also need a **buffer** that will be used for communication by the server. It should either be large or a growing buffer. The last thing you’ll need is a **UDP server created by network_create_server(network_socket_udp,{port},{maxplayers}**. All these will be fed into the **udphp_createServer** script.

**_How to use udphp_createServer (arguments)_**:

*   **server** - A UDP server
*   **buffer** - A buffer
*   **player-list** - A ds_list that will store all players (more information below)

**udphp_createServer** will return either true or false. If the returned value is false, the server creation failed.

```
player_list = ds_list_create();
buffer = buffer_create(256, buffer_grow, 1);
server = network_create_server(network_socket_udp,1234,32);
ret = udphp_createServer(server,buffer,player_list);
if (!ret) {
    //Server could not be created. Destroy instace. GMnet PUNCH will also show a message if not silent.
    instance_destroy();
}

```

###Server step event

**In obj_server’s step event** the actual magic happens. Just run **udphp_serverPunch** with no arguments.

###Server networking event

**And in obj_server’s networking event** we share the magic: Simply run **udphp_serverNetworking** with no arguemnts.

###Server: Client identification

**To identify clients** in the networking event, you take the **ip** and the **port**of **async_load** and check if they are in the player list you created earlier. The player list stores keys in the format “ip:port”.

####To see if a player is in the player list:

```
var in_ip = ds_map_find_value(async_load, "ip");
var in_port = ds_map_find_value(async_load, "port");
var exists = ds_list_find_index(player_list, in_ip+":"+string(in_port));
//exists will give you the position of the player in the list or -1 if he's not in there

```

####To get ip and port of a player entry:

```
var entry = /* Entry from the player list */
var ip = udphp_playerListIP(entry);
var port = udphp_playerListPort(entry);

```

To send a message to all players iterate over the player list and send a packet to all players (see hello world demo in step event).


---

**» Next topic: [Client](tutorial/4_client)**

« Previous topic: [obj_control](tutorial/2_obj_control)
