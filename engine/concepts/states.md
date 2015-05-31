States of the engine
--------------

The engine can be in different states.

1. Is the engine running (=Server or Client started)? -> [htme_isStarted](functions/tools/htme_isStarted) returns true
2. Are we running the server? -> [htme_isServer](functions/tools/htme_isServer) returns true
3. (Only client) -> Is the client connected to a server? -> [htme_clientIsConnected](functions/tools/htme_clientIsConnected) returns true
4. (Only client) -> Did a connection to the server fail? -> [htme_clientConnectionFailed](functions/tools/htme_clientConnectionFailed) returns true