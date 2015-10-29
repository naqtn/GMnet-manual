##11. チャット

この章ではプレーヤー間で情報を同期する新しい方法を学びます。
この方法はチャット（日：おしゃべり）メッセージや、それに似たもののために設計されています。
（訳注：ここの記述は、
ゲーム中でのチャット機能、
すなわちオンラインゲームでのプレーヤー同士が文字でコミュニケーションを取る機能はもちろん、
それに限らず、それと似た形で実現できる機能にこの章で述べる方法が使える、
ということを意味しています。）

これには [CHAT](concepts/chat) (Custom Handler for Advanced Traffic) と呼ばれるインターフェースを使います。
（訳注：略の元の形の訳は省略。無理やり頭文字を合わせた語でさして意味は無いので。）

この章ではこれをどのように使うかを説明します。
 [Bonus 5 - RPC](tutorial/17_rpc) の章では、より応用的な使用方法を扱います。

初めに**objectを作り``htme_obj_chat``と名づけます**。

（訳注：次の段はこれから書くプログラムの流れの概説なのですが、
原文が子細に見ると不明瞭で、また読み飛ばしても問題ないかと考え、訳すのをあきらめます。）
We are storing messages in the variable **message**. Or at least **the last** message sent by a player. Then we are **syncing it** via the engine, and the **local instance** of that object **will loop through all chat instances**, like we learned when creating the chat overlay. It will then **look for new messages in our "inboxes"**, and **add them to a list that contains all messages**.


###CHAT ハンドラの追加

**Create-Event** を作り次のコードを追加します：

```gml
mp_syncAsChatHandler("Chat");

//Setup variables
self.output = ds_list_create();
```

関数 **[mp_syncAsChatHandler](functions/chat/mp_syncAsChatHandler)** は
**"Chat"** チャンネルでの **文字列メッセージの送り手と受け手として、この object を登録**します。
**[mp_sync](functions/chat/mp_sync)**はここでは不要です。
object 自体を同期したいのではなくメッセージだけを同期したいからです。
すぐにそれが何を意味しているか分かるでしょう。

ds_list である**output**は**全てのチャットメッセージを保存する**のに使います。


###メッセージを送信

C キーの入力でメッセージを送るようにしたいと思います。
**press C-key Event** を作成し、次のコードを書き込みます：

```gml
self.str_id = get_string_async("Send a chat message:","");
```

このスクリプトは
**プレーヤーにチャットメッセージを問い合わせる**（訳注：文字入力をする）のに
*``get_string_async``**を使っています。
（訳補：この関数を）使ったことが無いなら少々込み入っているように感じるかもしれません。説明させてください：

``get_string_async``は``get_string``関数での文字列入力に似ていますが、
テキスト入力を行う箱（訳注：入力欄）の表示をゲームの進行を止めることなく行います。
（訳注：async は asynchronous（日：非同期性の）の略。詳しくは後で解説します。）
この（訳補：止めないという）ことは重要です。なぜならゲームの進行を止めると
（訳補：GMnetの）クライアントやサーバは接続を失ってしまうからです。
（訳注：一定時間の間通信できない状態が続くと、どこかで回線が切れたと判断するようになっているためです。）  
``get_string_async`` は（訳補：ユーザーが入力した）メッセージを返す代わりに、
番号を返すので保存しておきます。
入力したメッセージは **Asynchronous - Dialog Event** を作り、
次のようにして取り出します：

```gml
///Process the message the player typed in
var i_d = ds_map_find_value(async_load, "id");
if (i_d == self.str_id) {
   if (ds_map_find_value(async_load, "status")) {
      if (ds_map_find_value(async_load, "result") != "") {
         var message = ds_map_find_value(async_load, "result");
         //Send the message using the CHAT Interface.
         mp_chatSend(message);
      }
   }
}
```

（訳注：``async_load`` は GML で定義されているグローバル変数です。
非同期イベントが起きた際に、そのイベントに関する情報を保持しています。

GMnet の解説の範疇を外れますが、このあとの文章の理解の助けとすべく非同期処理について概説します。
一般にプログラミング言語における「非同期性（英：asynchronous、あしんくろなす）」とは、
何らかの処理実行依頼を行った際に、
その呼び出しが終了して呼び出し側の次のステップに実行制御が戻ってきた時点で、
依頼した処理がまだ完了していない可能性のある機能提供のしかたを指します。
non-blocking（のんぶろっきんぐ、日：非ブロック）と表現することもあります。

対義語は「同期性（英：synchronous）」で、
呼び出しが終わった時には既に処理が終わっています。

ここの例では ``get_string`` は同期性の関数で、
この関数から戻ってきた時点で既にユーザーによる文字列入力は完了しています。
一方``get_string_async``は非同期であって、
これはユーザーによる文字列入力の指示をしただけで関数から戻ってきていて、
「文字列を得る」という動作は終了していません。

これはリアル世界の店舗のカウンターで注文してから準備にしばらく時間が掛かるような場合に、
一旦番号札を受け取って待機し、
あとから呼び出しがかかって番号札と照合して品物を受け取るのと同じ方式です。
非同期方式では、
待機している間は別の事をしていても良いので時間利用の自由度が増します。
その代わり番号の授受、呼び出し、番号の確認のための仕掛けが増えて、手続きの複雑さは増します。
（訳注終わり））


これは少し込み入っていると思うかもしれません。
プログラムコードは入力されたメッセージが有効かどうかを確認します。
重要なのは最も内側の if 節の内側です。

``var message = ds_map_find_value(async_load, "result");``
はメッセージを取り出してローカル変数 **message** に格納します。

**[mp_chatSend(message)](functions/chat/mp_chatSend)** を使って
メッセージを全てのプレーヤに送信します。
このメッセージは同時に自分自身にも送信されます。


###メッセージを受信

（訳補：エンジンはメッセージを）受信すると ds_queue に格納します。
（訳補：今作成している``htme_obj_chat``は）毎stepで新たなメッセージが到着しているかを検査することにします。

**step event に次のコードを追加します**:（訳注：次は最初の３行だけで、この先にまだ続きます。）

```gml
var queue = mp_chatGetQueue();
while (ds_queue_size(queue) > 0) {
    var raw_message = ds_queue_dequeue(queue);
```

最初の行は [mp_chatGetQueue](functions/chat/mp_chatGetQueue) をメッセージのキューを得るのに使い、
つぎに**キューが空になるまでループ**します。
``ds_queue_dequeue``は最も古い**メッセージ**をキューから取り出しキューから削除します。

この（訳補：キューから取り出した）メッセージは“エンコード”されています。
二つの関数を使ってデコードします:

```gml
    var sender = htme_chatGetSender(raw_message);
    var message = htme_chatGetMessage(raw_message);
```

[htme_chatGetSender](functions/chat/htme_chatGetSender) と
[htme_chatGetMessage](functions/chat/htme_chatGetMessage) は
名前がほのめかすように、メッセージの著者（プレーヤーのハッシュ文字列）と送られたメッセージ文字列を返します。


メッセージは得られました。次は？  
プレーヤー object に名前を与えたのは覚えていると思います。
送られたメッセージと共に（訳補：メッセージを送ってきた）**プレーヤの名前を表示したい**と思います。  
そのためにまずプレーヤーのハッシュ文字列を使ってプレーヤーの名前を得ます。

```gml
    var player_instance = htme_findPlayerInstance(htme_obj_player,sender);
     if (player_instance != -1) {
         var name = (player_instance).name;
     } else {
         var name = "(Someboy in another room)";
     }
```

これは[9章](tutorial/9_playerlist)のと同じです。詳しくはそちらを参照してください。

最後にやる事は受信メッセージとそれを誰が送ったかをコロンで連結して、
create event で作成したリストに追加することです。

```gml
    //Add to list of chat output
    ds_list_add(self.output,name+": "+message);
}
```


###メッセージの表示

チャット・メッセージを表示するのに
次のコードを**draw-event**に追加します:

```gml
if (!htme_isLocal()) exit; //Again, exit if not our instance

//Get an offset, so we draw the newest line on bottom
var size = ds_list_size(self.output);
var bottomLine = room_height-50;
var offset = size*20;

for(var i = 0;i<size;i++) {
    var line = ds_list_find_value(self.output,i);
    draw_text(50,bottomLine-offset+i*20,line);
}
```

draw event はエンジンにとって重要な部分ではないので、ここでは説明しません。
簡単に言うと output 変数のリストに対してループし、それぞれの行を表示しています。

（訳注：ぱっと見、少々読みにくいので簡単に説明します。
この表示は１メッセージを１行に表示します。
１行は20ピクセルとしています。
最後の（つまり最新の）メッセージが来る位置を bottomLine 、
全メッセージを表示した場合に必要な高さを offset として計算し、
全メッセージの先頭座標を(bottomLine-offset)と求め、
そこを0番目としてyが増える方向に座標を計算しています。

ここまでで示した実装では output は溜まっていく一方なので、
画面に収まらない上部の描画は無駄になっています。
実用では一定数以上にならないようにする工夫が必要でしょう。）


完了です。テストしてみてください！



###プライベート・メッセージ

特定のプレーヤに向けたプライベート・メッセージを送ることも出来ます。
[mp_chatSend](functions/chat/mp_chatSend) は第二引数も指定できて、
ここにメッセージを送りたい特定のプレイヤーのハッシュを指定します。試してみてください！


---
##11. Chat

In this chapter you will learn a new way of syncing information between players. This method was designed for chat messages and similiar things.

For this we use the so called [CHAT](concepts/chat) (Custom Handler for Advanced Traffic) Interface. You will learn how to use it in this chapter and can find more advanced usages of it in chapter [Bonus 5 - RPC](tutorial/17_rpc).

First, let's **create an object ``htme_obj_chat``**. 

We are storing messages in the variable **message**. Or at least **the last** message sent by a player. Then we are **syncing it** via the engine, and the **local instance** of that object **will loop through all chat instances**, like we learned when creating the chat overlay. It will then **look for new messages in our "inboxes"**, and **add them to a list that contains all messages**.

    ??? Or at least **the last**
    ??? Do you mean that the message variable can hold only one string entered by user?
    ??? If so, I think there's need to emphasize "at least" and/or "the last".

    ??? "chat instances" what is it? chat queue element(or raw_message)?

    ??? "like we learned when creating the chat overlay"
    ??? Do you mean "player overlay" ?

###Adding a CHAT handler

Create a **Create-Event** and add the following code:

```gml
mp_syncAsChatHandler("Chat");

//Setup variables
self.output = ds_list_create();
```

**[mp_syncAsChatHandler](functions/chat/mp_syncAsChatHandler)**. This function **registers the object to be a sender and reciever for string messages** for the chanel **Chat**. *[mp_sync](functions/chat/mp_sync)* is not needed here. We won't be syncing the object itself, only messages. But you'll see what that means in a second.

    ??? Why italic for "[mp_sync]" ?

The ds_list **ouput** is used to **store all chat messages**.

###Sending a message.

We are going to send a message when the player presses the C-key. Create a **press C-key Event**:

```gml
self.str_id = get_string_async("Send a chat message:","");
```

This script uses **``get_string_async``** to **ask the player for the chat message**. If you never used that before, things might be a bit complicated, so let me explain:

``get_string_async`` displays an input box where the player can input text without locking the game, like ``get_string`` would do. That's important, because the client or server will loose connection, if the game is locked.  
Instead of returning the message, ``get_string_async`` returns a number, that we need to store. Inside the **Dialog Event, which can be found under Asynchronous** we are retrieving the message:

```gml
///Process the message the player typed in
var i_d = ds_map_find_value(async_load, "id");
if (i_d == self.str_id) {
   if (ds_map_find_value(async_load, "status")) {
      if (ds_map_find_value(async_load, "result") != "") {
         var message = ds_map_find_value(async_load, "result");
         //Send the message using the CHAT Interface.
         mp_chatSend(message);
      }
   }
}
```

    ??? why call ds_map_find_value twice?

This may seem a bit complicated, the code checks that the message entered was valid, but the important code is the code in the most inner if-clause.

``var message = ds_map_find_value(async_load, "result");`` retrieves the message and writes it to the local variable **message**.

Using **[mp_chatSend(message)](functions/chat/mp_chatSend)** we are now sending this message to all players. It will also be sent to ourself.

###Recieving messages

Messages are stored in a ds_queue, which is filled when new messages arrived. We will be checking every step if new messages arrived.

**In the step event, add the following code**:

```gml
var queue = mp_chatGetQueue();
while (ds_queue_size(queue) > 0) {
    var raw_message = ds_queue_dequeue(queue);
```

The first line uses [mp_chatGetQueue](functions/chat/mp_chatGetQueue) to get the queue of messages and then **we loop through it until it is empty**. ``ds_queue_dequeue`` will **get** the oldest **message** in the queue and remove it from the queue.

This message however is "encoded", so we now use two functions to decode it:

```gml
    var sender = htme_chatGetSender(raw_message);
    var message = htme_chatGetMessage(raw_message);
```

[htme_chatGetSender](functions/chat/htme_chatGetSender) and [htme_chatGetMessage](functions/chat/htme_chatGetMessage) will, as their name might suggest, return the author of the message (the hash of the player) and the sended message.

So now we have the message. What now?  
As you may remember, we gave all our player objects names. **We want to display the sent message together with the name of the player**.  
To do that, we first have get the name of the player object using the player hash:

    ??? "we first have get" "have to get"?

```gml
    var player_instance = htme_findPlayerInstance(htme_obj_player,sender);
     if (player_instance != -1) {
         var name = (player_instance).name;
     } else {
         var name = "(Someboy in another room)";
     }
```

This is the same as in the [chapter 9](tutorial/9_playerlist), so check this page of the tutorial for more information.

The last thing we do, is we add the message we recieved to the list we created in the create event, together with who sent it, seperated by a ":".

```gml
    //Add to list of chat output
    ds_list_add(self.output,name+": "+message);
}
```


###Display the chat.

To display the chat, put the following code into the **draw-event**:

```gml
if (!htme_isLocal()) exit; //Again, exit if not our instance

//Get an offset, so we draw the newest line on bottom
var size = ds_list_size(self.output);
var bottomLine = room_height-50;
var offset = size*20;

for(var i = 0;i<size;i++) {
    var line = ds_list_find_value(self.output,i);
    draw_text(50,bottomLine-offset+i*20,line);
}
```

That draw event is not essential part of the engine, so I'm not explaining it here. It basically loops over the output list and displays each line.

We are done. Have fun testing it out!

###Private messages
You can also send private messages to certain players. [mp_chatSend](functions/chat/mp_chatSend) supports a second argument, where you can use the hash of a player to only sent your messages to specific players. Try it out!

---

**» Next topic: [Conclusion / What's next](tutorial/12_end)**

« Previous topic: [Adding day/night](tutorial/10_time)
