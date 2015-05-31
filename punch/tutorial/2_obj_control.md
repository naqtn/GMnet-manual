##2. obj_control

Let’s actually talk about this “behaviour”:
I will not go over the debug objects in the sample project, I will only guide you through the neccassry objects/code.
Let’s start with object **obj_control**. The only important thing in _obj_control_ is the **create event**.
In the create event you can find, that **udphp_config** is called. This is the **first** you have to call when you want to use GMnet PUNCH.

**How to use udphp_config (arguments)**:

*   **master_ip(stringl)** -> The IP of the master server that both server and client will use to connect to each other. Confused? See the section _Wait, I need to host a “master server”?! - Where do I get that?_.
*   **master_port(real)** -> The UDP and TCP port the master server listens on.
*   **reconnect intverval(real)** -> After this amount of steps the server will reconnect to the master server. This has to be done, to ensure the server is always connected to the master server. Future versions will auto-reconnect on loss of connection, but we are still testing that out.
*   **connection timeout(real)** -> After this amount of time the server and client will give up to connect t eachother. The client will display a connection failed message. This timeout will also be used if you set the client to directly connect to the server.
*   **debug(boolean [0/false or 1/true])** -> Show more debug messages. Not recommended for production use.
*   **silent(boolean)** -> This will turn ALL debug messages off. Recommended for production use.

Copy the call of this script to your game startup or somewhere else where it get’s called before the other GMnet PUNCH scripts. Make sure no global variables starting with udphp_ are used. These are reserved for _GMnet PUNCH_.

---

**» Next topic: [Server](tutorial/3_server)**

« Previous topic: [Implementing GMnet PUNCH in your game](tutorial/1_intro)
