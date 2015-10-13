##4. エンジンを開始する

よっしゃ！準備は出来ました。では実際にゲームを作っていきましょう。

始める前に、このチュートリアルの手順を実際に追おうとするなら、
前に述べたように空のプロジェクトに全ての sprites 全ての scripts と
``obj_htme`` object を追加してある事を確認してください。

（訳注：以下では、
ゲームプログラムの中で GMnet によって実現されるクライアント機能部分を「クライアント」、
サーバ部分を「サーバー」と表現しています。別途のプログラムやマシンがあるわけではありません。）

### メニュー
とても基本的なメニューを作りましょう。

まず **新しい room** を作り **htme_rom_menu** と名づけます。
（訳注：htme は共通のプレフィックス、続く rom は room を表しています。全体的にこの命名方針をとるようです。）

このチュートリアルでは、
プログラムを（訳補：複雑にせず）ごく基本的な状態を維持するよう努め、**他のビューは使わない** ようにします。
 **background color** は **black** にして room の大きさは **800×600** ピクセルにします。

**``obj_htme``** を room に追加します。
この object をゲームの最初の room で作るようにします。
これは永続的（persistent）であって、room を変更しても存在し続けます。
（訳注：obj_htme のプロパティを見ると Persistent にチェックが入っていることが確認できます。）

（訳補：つぎに新たな）object を **作成** し **``htme_obj_menu``** と名づけます。
これはメニューを制御します。さきほど作った room に追加します。

**Draw-Event** に次のコードを追加します。
これはゲームを開始した時にどうやって先に進めるかの簡単なメッセージを表示します：

```gml
draw_text(20,20,"Press N for new server and B to connect.");
```
（訳：キーボードで選択（N: 新たなゲーム・サーバになる, B:ゲーム・サーバに接続する））

さらに二つのイベントを追加します。
**B-key** イベントと **N-key** イベントです。
**B** はゲーム・サーバに接続し  **N** は新規にゲーム・サーバを作ります。


####サーバの開始

**N-key** イベントに次のコードを追加します：

```gml
///START SERVER

//Ask player for port
var port = real(get_string("On which port should the server listen?","6510"));

//Setup server, on success start game, on failure end the game.
if (htme_serverStart(port,32)) {
    room_goto(htme_rom_demo);
} else {
    show_message("Could not start server! Check your network configuration!");
    game_end();
}
```
（訳：プレーヤーにポートをたずねる）
（訳："サーバーが使用するポート番号は？"）
（訳：サーバーを開始する。成功したらゲームを開始、失敗したらゲームを終了）
（訳："サーバーを開始出来ませんでした。ネットワークの設定を確認してください。"）

まず **どのポートで** サーバが動くべきか **プレーヤーにたずねて** います。
（もちろん、固定のポート番号を使用することにしてもかまいません。）

その後 ``htme_serverStart(port,maxplayers)`` を使って **サーバーを開始** しています。
ポート番号を指定し、接続最大数を **32 プレーヤー** にしています。
サーバーが動作しているかを確認し動いているなら、この後すぐに実装する **game room へ移動** しています。


####クライアントの開始

**B-key** event には次のコードを追加します：

```gml
///CONECT TO A SERVER

//Ask player for ip & port
var ip = get_string("To which server should we connect?","127.0.0.1");
var port = real(get_string("And on which port is the server running?","6510"));

//Setup client, on success go to waiting room, otherwise end game
if (htme_clientStart(ip, port)) {
    room_goto(htme_rom_connecting); //NOTE THAT WE ARE GOING TO ANOTHER ROOM HERE THAN THE SERVER ABOVE
} else {
    show_message("Could not start client! Check your network configuration!");
    game_end();
}
```
（訳："どのサーバーに接続しますか？"）
（訳："そのサーバーはどのポート番号で動作していますか？"）
（訳：クライアントを設定する。成功なら waiting room へ。そうでなければゲームを終了。）
（訳：注意。ここでは上のサーバ（訳補：のコード）とは違う別の room へ移動する）


今度は少し込み入っています。
**IP アドレスとポート番号の両方** をたずねた後、
``htme_clientStart(ip, port)`` を使って接続を試みます。

（訳補：サーバーの場合は）game room へ移動したのに対して、
**クライアントでは** これから作る別の room である ``htme_rom_connecting`` へ移動します。
（訳補：それは）何故なのか？
この room は **接続中というメッセージを表示** し、
**クライアントが接続するのを待つ** ための object を保持します。
（訳補：接続が完了した）**その後に** game room へ移動します。
医者での **待合室（waiting room）** と同じような感じです。


#####waiting room （待合室） ``htme_rom_connecting``

**room を作り**  ``htme_rom_connecting`` と名づけます。
初めのと同じように新たな **object を作り** ``htme_obj_waitforclient`` と名づけ、
この **room に追加** します。

（訳補：この object の）**Draw event** に次のコードを書きます：
```gml
draw_text(20,20,"Connecting...");
```

これは（訳補：前の room で）プレーヤーがクライアントを開始するのを選択した後に、
"Connecting..." というメッセージを表示します。

（訳補：この object の）**Step-Event** に次のコードを書きます：

```gml
///Check if client is connected
if (htme_clientIsConnected()) {
    room_goto(htme_rom_demo);
}
if (htme_clientConnectionFailed()) {
    show_message("Connection with server failed!");
    game_restart();
}
```

最初の文の ``htme_clientIsConnected()`` 関数は、
クライアントがうまく接続しているかを調べます。
接続しているなら **game room へいよいよ移動** します。

（訳補：接続しないまま） ``global_timeout`` （[設定](tutorial/1_config)の節参照）に達すると
エンジンは接続を諦めます。
この場合、失敗を確認する関数 ``htme_clientConnectionFailed()`` を使う二番目の if 文 が成立し、
このコードの場合はゲームをリスタートさせています。

この waiting room は一つの例であって、接続中のメッセージを表示するのに他の技法を使うこともできます。


##接続完了！

理論的には、これでもうゲームがプレイできます。
とはいえもちろんまだゲーム本体を実装していませんが。
ゲーム（訳補：本体の） room ``htme_rom_demo`` はまだ存在していないので、
（訳補：メニューでNキーを選択して）ゲーム・サーバを開始しようとするとプログラムはクラッシュします。

では、以前やったように **空の room を作り**  ``htme_rom_demo`` と名づけましょう。

これでプログラムを二重に起動すると（訳注：一つを動かしたまま同じプログラムをもう一回実行する、ということ）、
一方では（訳補：N キーで） **ゲーム・サーバを開始** でき、（訳補：今作った） **空の room に達する** でしょう。

**もう一方** では、**IP アドレス 127.0.0.1** で **このゲーム・サーバに接続** 出来るでしょう。
もし（訳補：接続に）成功すると、（訳補：接続中を表す）"Connecting..." のメッセージは消え、
**同じ空の room に達する** でしょう。**ヤッター！**

（訳注：GameMaker: Studio の メニュー Run から二重に起動はできないので、
メニュー File > Create Application... を使って実行形式を書き出して、
一つはそちらを実行することになるでしょう。）

---
##4. Starting the engine

Great! Now that we are set up, let's actually make a game.

Before we start, if you want to follow the tutorial make sure again, that you added all sprites, all scripts and the object ``obj_htme`` to an empty project.

###The menu
Let's create a very basic menu.

First create a **new room** called **htme_rom_menu**. For this tutorial we are keeping things very basic and we are **not using any views**. Set the **background color** to be **black** and the dimensions of the room to be **800*600**px.

    ??? "800*600"
    ??? I suggest replace "*" with "x" as it is so in 5_platformer.md.

Add **``obj_htme``** to the room. This object should be created in the first room of every game you create. It is persistent and will exist even when you change the rooms.

Now **create** an object called **``htme_obj_menu``**. This will control our basic menu. Add it to the room we just created.

In the **Draw-Event** put the following code, that will simply display a message on how to proceed when starting the game:

```gml
draw_text(20,20,"Press N for new server and B to connect.");
```

Add two more events to it. One **B-key** event and a **N-key** event. **B** will join a server and **N** create a new one.

####Starting the server

In the **N-key** event add the following code:

```gml
///START SERVER

//Ask player for port
var port = real(get_string("On which port should the server listen?","6510"));

//Setup server, on success start game, on failure end the game.
if (htme_serverStart(port,32)) {
    room_goto(htme_rom_demo);
} else {
    show_message("Could not start server! Check your network configuration!");
    game_end();
}
```

This will first **ask the player** on which **port** the server should run (of course you can also decide to specify a fixed port number).

After that it **starts the server** using ``htme_serverStart(port,maxplayers)`` on that port and allows a maximum of **32 players**. It checks if the server is running, and if it is, it **goes to the game room** that we will create in a second.

####Starting the client

In the **B-key** event add the following code:

```gml
///CONECT TO A SERVER

//Ask player for ip & port
var ip = get_string("To which server should we connect?","127.0.0.1");
var port = real(get_string("And on which port is the server running?","6510"));

//Setup client, on success go to waiting room, otherwise end game
if (htme_clientStart(ip, port)) {
    room_goto(htme_rom_connecting); //NOTE THAT WE ARE GOING TO ANOTHER ROOM HERE THAN THE SERVER ABOVE
} else {
    show_message("Could not start client! Check your network configuration!");
    game_end();
}
```

Now that is slightly more complicated. It **asks for both ip and port** and then tries to connect using ``htme_clientStart(ip, port)``.  
Now instead of going to the game room when we are done, we actually want **the client to go to** ``htme_rom_connecting`` which is a room we are now going to create. Why? This room will **display a message saying "*Connecting...*"** and there will be an object in it that w**aits for the client to be connected**. **After** that we want to go to the game room. It's like the **waiting room** at the doctor.

    ??? "w**aits"
    ??? "w" must be inside of bold styling.

#####The waiting room ``htme_rom_connecting``
**Create a room** called ``htme_rom_connecting`` that is just like the first one (but without the objects in it). Now **create the object** ``htme_obj_waitforclient`` and **place it** into the room.

In the **Draw event** put the following code:
```gml
draw_text(20,20,"Connecting...");
```

This will display the message "Connecting..." after the player decided to start the client.

In the **Step-Event** put the following:

```gml
///Check if client is connected
if (htme_clientIsConnected()) {
    room_goto(htme_rom_demo);
}
if (htme_clientConnectionFailed()) {
    show_message("Connection with server failed!");
    game_restart();
}
```

The first statement used the ``htme_clientIsConnected()`` function to check if the client is... well connected. If so, **we can finally go to the game room**.  
If the global timeout has been reached, the engine gives up to conect. In this case the second if-Statement is activated which uses ``htme_clientConnectionFailed()`` to check if the connection failed. In our example it will simply restart the game.

    ??? "global timeout"
    ??? I think it's better to write it as ``global_timeout`` and refer 1_config.md Configuration section.

This waiting room is just an example and you can use different techniques to display a waiting... message.

##Connection done!

Theoretically, we could now play the game. Of course, there is no game. The game will crash if we try to start a server because our game room ``htme_rom_demo`` does not exist.

For now, **create an empty room** just like you did before and call it  ``htme_rom_demo``.

Now, when you **fire up your game twice**, you should be able to **start a server** on one game, which should **lead you to the empty room**.

On the **other game** you should be able to **connect to this server** by connecting to the ip **127.0.0.1**. If it was successfull, the "Connecting..." message should disappear, and you'll **find yourself in the same empty room as the server**. **Yay!**

---

**» Next topic: [Setting up the basic platformer](tutorial/5_platformer)**

« Previous topic: [**PLUS** - Hosting a master server](tutorial/3_udphp2)
