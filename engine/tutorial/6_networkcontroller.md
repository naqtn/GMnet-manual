##6. ネットワーク・コントローラ

先に進める前に、
エンジンが正常に動作しているかどうかを分かるようにする object を作成しましょう。

サーバとクライアント間 ** 接続 ** が ** 失われる ** と、
クライアント側の ** エンジンは停止 ** します。


``htme_obj_network_control`` という名前で ** object ** を作り、
**Step-Event** に次のコードを書きます：

```
///Check if engine running
if (!htme_isStarted()) {
    show_message("Game Server or Client died! Restarting game...");
    game_restart();
}
```

（訳：エンジンが動いているか検査する）
（訳：ゲーム・サーバあるいはクライアントが停止！ゲームを再起動します...。）


クライアントがゲームサーバに接続した後で
``htme_isStarted()`` 関数が ** false を返した ** ならば、
サーバへの ** 接続が失われた** のだと判定できます。

この状況を扱うコードは（訳補：必要なら）この if 文の中に書きます。
サーバ（訳補：動作するエンジン）では、
エラーによってサーバーが停止しない限り ``htme_isStarted()`` は常に true を返します。

あ、そうそう、この object を ``htme_rom_demo`` room に置くのを忘れないでください。


---
##6. The network controller

Before we continue, let's create an object that makes sure, the engine is still running.

The **engine will stop** running on the client-side, when the **connection** between server and client is **lost**.

**Create the object** ``htme_obj_network_control``. Into the **Step-Event** put the following code:

```
///Check if engine running
if (!htme_isStarted()) {
    show_message("Game Server or Client died! Restarting game...");
    game_restart();
}
```

If ``htme_isStarted()`` **returns false** at any point after your client connected to the server, you can be very certain, that you **lost conection** to the server. Into the if Statement, simply put your own code to handle this scenario. ``htme_isStarted()`` should always return true for the server, unless the server dies due to an errror.

Oh, and don't forget to put the object into the ``htme_rom_demo``.

---

**» Next topic: [Adding a player](tutorial/7_player)**

« Previous topic: [Setting up the basic platformer](tutorial/5_platformer)
