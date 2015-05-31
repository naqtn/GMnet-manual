##Function reference

_These are very brief and incomplete information. Detailed information can be found in the script files_

The following scripts are scripts **YOU as the game developer** use:

### Setup:

*   **udphp_config**  
    One-time setup script  
    Usage: udphp_config(master_ip,master_port,reconnect_intv,timeouts,debug,silent)

### Server:

*   **udphp_createServer**  
    To be used in the Create event of the server  
    Usage: udphp_createServer(udp_server,buffer,player_list)
*   **udphp_serverPunch**  
    To be used in the step event of the server  
    Usage: udphp_serverPunch()
*   **udphp_serverNetworking**  
    To be used in the networking event of the server  
    Usage: udphp_serverNetworking()
*   **udphp_stopServer**  
    Usage: udphp_stopServer()  
    Delete the instance afterwards

### Client:

*   **udphp_createClient**  
    To be used in the Create event of the client  
    Note: Returns client id  
    Usage: udphp_createClient(udp_socket,server_ip,buffer,directconnect,directconnect_port)
*   **udphp_clientPunch**  
    To be used in the step event of the client  
    Usage: udphp_clientPunch(id)
*   **udphp_clientNetworking**  
    To be used in the networking event of the client  
    Usage: udphp_clientNetworking(id)
*   **udphp_stopClient**  
    Usage: udphp_stopClient(client_id)  
    Instance should be deleted with the false return value of clientPunch

### Tools:

*   **udphp_clientGetServerIP**  
    [for client] This will return the server ip of this client and should only be used if the client is connected.  
    Usage: udphp_clientGetServerIP(client_id)
*   **udphp_clientGetServePort**  
    [for client] This will return the server port of this client and should only be used if the client is connected.  
    Usage: udphp_clientGetServerPort(client_id)
*   **udphp_playerListIP**  
    [for server] Get an ip out of a player list entry (see serverCreate for details)  
    Usage: udphp_playerListIP(player)
*   **udphp_playerListPort**  
    [for server] Get an port out of a player list entry (see serverCreate for details)  
    Usage: udphp_playerListPort(player)
*   **udphp_clientIsConnected**  
    [for client] With this you can check if your client has conncted to the server.  
    Usage: udphp_clientIsConnected(client_id)
    
### Lobby:
*   **udphp_downloadServerList**  
    [no server or client has to be running]  
    Download a list of servers from the lobby. [More information](tutorial/5_lobby).  
    Usage: [See GMnet ENGINE manual page](http://gmnet.parakoopa.de/manual/engine/functions/lobby/udphp_downloadServerList)
