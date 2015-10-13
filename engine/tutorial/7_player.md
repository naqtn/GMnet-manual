##7. プレーヤーを追加する

ええはい、ステップ 5 でプレーヤーを既に追加したのは分かっています。

このタイトルが意味しているのは、
今度は **エンジンにプレーヤを追加する** という事です。
このステップが終わると、プレーヤーが
**サーバに接続している全てのプレーヤーの間で同期** するようになります。
なので、このステップが終わると基本的には（訳補：チュートリアルは）完了します。
残りはいくらか高度な話題に関するものです。

（訳注：この節の説明で「プレーヤー」という言葉が、
「ゲーム・プログラムにおいて room に配置される object としてのプレーヤー」の意味と、
「ゲーム・プログラムで遊んでいる人としてのプレーヤー」
ないしは「その人の元で動かしているゲーム・プログラム」の少し異なった意味で
使われている。文脈によって区別は出来るがわかりにくい。
TODO 見直す。原著者に修正提案？）


###create event

プレーヤーをセットアップするには最低限の調整を行うだけです。
**create event に新たな Execute Action を追加し** 他のコードの **前に** 置きます。

（訳注：ステップ 5 で作成した初期化処理より前に配置します）


次のコードではじめます。（訳注：書き込むのはこれだけでなく後で出てくるコード片を順に書き連ねていくことになります。）
```gml
mp_sync();
```

これは **エンジンにこの object を同期することを伝えます** 。
この object のインスタンスが作られると、
そのインスタンスは（訳補：マルチプレイしている） **他の全てのプレーヤーの下に送られ** ます。

１つのプレーヤー・インスタンスを room に追加する場合で、
もし４人のプレーヤーが互いに接続しているとすると、
それぞれのプレーヤーは４つのプレーヤー・インスタンスを持つことになります。


次にエンジンに対して「どの変数を、どのように同期するか」を伝える必要があります：
```gml
mp_addPosition("Pos",5*room_speed);
```

これは、
位置（英語：position）の変数 ``x`` と ``y`` とを 5 秒ごとに同期することをエンジンに伝えています。
``5*room_speed`` は 5 秒を意味します。
``mp_addPosition`` の最初の引数は“グループ”の名前です。
この名前は好きなように付けられます。
（訳注：グループに position を含めるのでここでは "Pos" にしていますが別の文字列でも構いません。）

（訳補：この関数で）今追加したものは**変数グループ**（英語：variable group）と呼ばれるものです。
（訳補：この例の場合、）グループの名前は "Pos" で、
5 秒ごとに同期され、同期される変数は ``x`` と ``y`` です。

（訳注：同期される変数がインスタンス変数 ``x`` と ``y`` なのは、
mp_addPosition の仕様としてあらかじめそのように決まっているからです。
後で出てくる方法では利用者が変数を指定します。）


（訳補：では、）位置を **どのように同期するか** を設定しましょう：

```gml
mp_setType("Pos",mp_type.SMART);
```

これは変数グループ "Pos" の**同期タイプ**（英語：sync type）を変更します。
**デフォルトは FAST** で、
それをこの例では **SMART** に変更しています。
（訳補：設定可能な）それぞれの同期タイプが何をするかを次に一覧します：


* **FAST** （デフォルト値。FAST を使用するのであれば ``mp_setType`` を呼ぶ必要は無い）:
今回の例で FAST を選んだなら、
エンジンはプレーヤの位置を 5 秒ごとに **一度だけ** 送信します。
UDP を通信に使用しているので（訳注：UDP はインターネットで使用される通信方法の一つ。）
確実に届く保証はありません。
つまり 5 秒ごとに他のプレーヤーが実際に位置を受け取っているかは分かりません。
パケット（訳注：一度に送る情報の塊のこと。）は失われるかもしれません。
とはいえ、FAST はとても... はやいです。
この節で後ほど FAST を使用します。


* **IMPORTANT**:
IMPORTANT を使用すると、今回の例では同じく 5 秒ごとに位置は同期されます。
しかし
パケットが確実に届くようにする
 *GMnet ENGINE* の（訳補：中に実装された）特別な方法を使うことになります。
5 秒ごとに、
サーバーとクライアントは
（訳補：通信相手が）受領したとの返信を返してくるまで
情報をあふれんばかりに送りつけます。
これ（訳注：受領完了の受領まで送り続ける事）が確実に送られたことを保証する方法です。
これは通信がだいぶ重くなる操作で
短い間隔で実行すると接続とフレーム・レートの両方で延滞（英:lag, ラグ）を引き起こすでしょう。


* **SMART**:
これは IMPORTANT に似ていますが、まし（訳補：な方法）です。
5 秒ごとに同期する代わりに、
5 秒ごとに変化したものだけを同期します。
もし x 座標位置だけが変わったとすると、y 座標位置については同期しません。
位置が全く変わらなかったとすると、同期処理を行いません。
これは基本的には IMPORTANT の通信に優しい版です。


（訳補：このデモでは）比較的大きな時間間隔で **SMART** を使います。
後で見るように毎回の step でボタン入力を同期するので、
位置は（訳補：その）補助の目的で同期するからです。
同期できていない状態におちいっていない事を保証するためだけに位置を同期します。

（訳注：これは「ボタン入力がきちんと届いていれば、それぞれのプレーヤーのもとで同じ移動計算がされて、
結果的に位置も同じ値になるはず。ではあるが、それを補完するために時々位置を確実に送るようにする。」
という方式を取るという事です。今述べたことと同じ内容を次の段落で説明します。）

**ボタン入力は FAST で同期させます。**
これは、
送信パケットは（訳補：FAST なので）いくらか（訳補：宛先に届かずに）失われて、
ゲームの複雑さ次第ですが
少しの時間の後にはプレーヤーが完全に異なる状態になりうる事を意味しています。
そういうことが起きないように**位置を 5 秒ごとにリセットします**。

（訳注：不達が起きると例えば、
プレーヤーがぎりぎりジャンプに成功したのに、通信先では失敗するという計算結果になる、ということが起こります。
この方法は「そうなってしまうのは仕方ないとして、位置を設定しなおして復活させる措置を取る」ということです。）


5 秒ごとにリセットすれば、（訳補：パケットが失われても）
**何ピクセルかずれるだけ** となります。
その場合、リセットが起こるたびにプレーヤーが**少しばかりちらちら**するかもしれません。
**見栄え良くはありません。**

では少しばかり **tolerance range** （日：許容幅）を加えましょう。
次のコードで、
もし場所が**あるべき値からのズレが 20 ピクセルより小さいなら**、
他のプレーヤーのもとでは**この変更は適用されず**、
**ちらつきを起こさない**ようになります。

```gml
mp_tolerance("Pos",20);
```

よし。位置の設定については終わりました。
では、**基礎的な Game Maker の物理と描画のための変数** についても同期させましょう：

```gml
/**
 * Tell the engine to add the basic drawing variables:
 * image_alpha,image_angle,image_blend,image_index,image_speed,image_xscale
 * image_yscale,visible
 */
mp_addBuiltinBasic("basicDrawing",15*room_speed);
mp_setType("basicDrawing",mp_type.SMART);

/**
 * Tell the engine to add the builtin GameMaker variables:
 * direction,gravity,gravity_direction,friction,hspeed,vspeed
 */
mp_addBuiltinPhysics("basicPhysics",15*room_speed);
mp_setType("basicPhysics",mp_type.SMART);
```

（訳：エンジンに対して次の基礎的な描画の変数を追加する。）
（訳：エンジンに対して次の組み込み（英：builtin）変数を追加する。）

（訳注：以下の文章での「物理（英：physics）」という語は、
具体的には上記の direction ～ vspeed の変数で扱われる
GML の基本的な物理（英：basic physics）特性を表す変数を指しています。
一方、現在の GameMaker: Studio 環境では physics という語で、
より高度な衝突検出などを扱う機能を指していることがあります。
両者は別の範囲なので注意してください。
GameMaker: Studio のリファレンスマニュアルで言えば前者は
[Reference > Movement and Collisions > Movement](http://docs.yoyogames.com/source/dadiospice/002_reference/movement%20and%20collisions/movement/index.html) で、後者は
[Reference > Physics > Physics Variables](http://docs.yoyogames.com/source/dadiospice/002_reference/physics/physics%20variables/index.html)
です。ここでは前者のみを扱います。）


これらは頻繁にそれほど同期する必要はありません。
物理（訳補：特性を表す変数）を頻繁に同期すると奇妙に見えますし、
描画まわり（訳補：で同期が必要なの）はプレーヤーの色の ``image_blend``
（これは（訳補：create 時に決定してゲーム中には）変化しない）と、
どの方向を向いているかを制御する ``image_xscale`` と ``iamge_angle``
（これは（訳補：ゲーム進行上）さほど重要ではない）だけですし。


さて、あと **name を同期** したいですね：
```gml
mp_add("playerName","name",buffer_string,60*room_speed);
mp_setType("playerName",mp_type.SMART);
```

（訳注：ここまで同期の対象だったのはあらかじめ GML で定義された変数でした。
name は [step 5](tutorial/5_platformer) 独自に定義したもので、
ここからはその場合の説明になります。）

独自に定義した変数の同期のために ``mp_add`` を使っています。
書き方は少しばかり複雑になり、さらに、動くようにするには（この後述べますが）もう少し付け加える必要があります。
その前にまずはここで何をしているかを見て見ましょう：
* 第１引数は、前の例と同じようにグループの名前です。
* 第２引数は、同期したい**変数の名前**です。カンマで区切って複数指定できます。
  プレーヤの名前は "name" 変数に保存してい（訳補：るのでそれを指定し）ます。
* 第３引数は、 **buffer type** （日：バッファ・タイプ）です。
  指定できるバッファ・タイプの種類は [このマニュアルページ](concepts/buffer) に述べてあります。
  （訳注：変数が保持するデータの種類（型）を示す定数。GML の関数 buffer_write 等で使用されるものを流用。）
  （訳補：一回の mp_add でカンマ区切りで指定する）**全ての変数は、同じバッファ・タイプでなければなりません**。
  （訳補：この例で指定した）``buffer_string`` は "name" 変数が文字列を保持している事を意味しています。
* 最後の引数は、以前と同じで同期の時間間隔（英：interval、インターバル）です。


同期間隔は60秒にしました。
というのは、name は（訳補：このゲームの実装では create 時に決定された後は）決して変化しないからです。
これを20年にしても違いは有りません。（訳注：mp_add の次の文でSMARTを指定していて変化が無ければ送信しないので。）
間隔をいくつにしたとしても、
エンジンがログイン時（訳注：内部処理で言えばインスタンス生成）と他の重要なイベントの時に同期処理をし、
しかもそれは自動的に行われます。

（訳補：次の ``mp_setType`` 呼び出しでは）
これらのイベントの時にだけ同期されるように SMART を指定する必要があります。


次の話題は**制御**（英：control）です。
ボタン入力を個別の変数に保存していた事は覚えていますか？
ここでそれが何故なのか分かるでしょう:

```gml
mp_add("controls","pressed_jump,pressed_left,pressed_right",buffer_bool,1);
```

バッファ・タイプは``buffer_bool``です。
なぜならこれらの変数は真偽値（1または0、（訳補：定数で書けば）trueまたはfalse）だからです。

（訳補：間隔に1を指定しているので、）
これは**全てのプレーヤに対してフレーム（訳注：ゲームの処理ループの一回）毎に逐一（訳補：入力状態が）どうであれ、
ボタン入力を同期**します。
（訳補：mp_type は）SMART や IMPORTANT にはしません。
**FAST を選択すべきです**。
データが到着したかを確認する処理段階が無いからです。
毎回の step でボタン入力をいずれにせよ同期（訳補：しようと）するわけですから。

（訳注：ソースコードでは明示していませんが "controls" グループの mp_type はデフォルトの FAST になります。
ここで述べられているのは「毎フレーム送るのだから、到着を確認してうんぬんする必要が無い」ということです。
これは「届いていない時に再送処理をしようにも、次のフレームになれば新たに届く。
届かないとすればそれは通信の障害であって、その場合には再送処理も完遂できない。
よって FAST でばんばん送ればいい。」という理屈です。）



###``mp_add`` を使うときに必要な事

``mp_add`` を（GML で定義されているものでなく）独自の変数に使うので、
コードの変更をちょっとする必要があります。
step の開始時にエンジンに変数値を送り、終了時に取り出す必要があります。

その理由は、
GameMaker では
[変数名の文字列で変数の値を取得する方法が無い](http://gmc.yoyogames.com/index.php?showtopic=646036&hl=)からです。
エンジンが値を読む前に map （訳注：GMnet が内部で管理している GML に用意されている [DS map](http://docs.yoyogames.com/source/dadiospice/002_reference/data%20structures/ds%20maps/index.html) のこと。）に
まずは値を保存する必要があります。
これは
``mp_addPosition``, ``mp_addBuiltinBasic``, ``mp_addBuiltinPhysics`` の場合には必要ありません。
（訳注：変数名が既知なのでエンジンの中で）ハード・コードされているからです。

ここで何を言っているのか分からなくても心配しないでください。それは複雑なので（訳補：キニスンナ）。

**知っているべきことはただ、今から説明する（訳補：２つの）ことです：**

（訳補：その１）``mp_add`` を使う全ての object について、
**begin step** イベントに次を加える：
```gml
mp_map_syncIn("name",self.name);
mp_map_syncIn("pressed_jump",self.pressed_jump);
mp_map_syncIn("pressed_left",self.pressed_left);
mp_map_syncIn("pressed_right",self.pressed_right);
```

（訳補：もちろん）名前は同期しようとする変数の名前に変えてください。
これらは、このチュートリアルでの変数です。

これらの変数への変更は ``mp_map_syncIn`` の呼び出し**前に**する必要があります。
つまり、
変更は begin step の中で行う（訳補：そして上記コードを実行する）か、
変更したらもう一度 ``mp_map_syncIn`` を呼ぶ必要がある、ということです。
最初の方法を推奨します。そしてそれがこの後で説明しようとする内容です。

（訳補：その２）**end step** event に次の変数の値取り出すコードを書き加える：

```gml
self.name = mp_map_syncOut("name", self.name);
self.pressed_jump = mp_map_syncOut("pressed_jump", self.pressed_jump);
self.pressed_left = mp_map_syncOut("pressed_left", self.pressed_left);
self.pressed_right = mp_map_syncOut("pressed_right", self.pressed_right);
```


###同期のための制御（訳補：変数）の設定

最後に必要なのは
以前（訳補：[step 5](tutorial/5_platformer)で）実装した**step eventから次のコードを取り出す**ことです。

```gml
self.pressed_jump = keyboard_check(vk_space);
self.pressed_left = keyboard_check(vk_left);
self.pressed_right = keyboard_check(vk_right);
```

**単に取り除いてください**
（訳補：そして）begin step の他のコードの **前に**、**次のコードを追加**します。

```gml
if (htme_isLocal()) {
    self.pressed_jump = keyboard_check(vk_space);
    self.pressed_left = keyboard_check(vk_left);
    self.pressed_right = keyboard_check(vk_right);
}
```

すると（訳補：begin step のコードは全体として）このようになります：

```gml
if (htme_isLocal()) {
    self.pressed_jump = keyboard_check(vk_space);
    self.pressed_left = keyboard_check(vk_left);
    self.pressed_right = keyboard_check(vk_right);
}
mp_map_syncIn("name",self.name);
mp_map_syncIn("pressed_jump",self.pressed_jump);
mp_map_syncIn("pressed_left",self.pressed_left);
mp_map_syncIn("pressed_right",self.pressed_right);
```

ここで begin step の最初に書いた事はつまり、
**ローカルで作成されたインスタンスかを検査し** そして
**プレーヤーのボタン入力を変数に書き込む** ということです。

（訳注：ここでの「ローカル」はネットワーク・プログラミングで言うところの
「通信をしているこちら側、今このプログラムを動かしている側」という意味です。
対義語は通信相手を指す「リモート」です。）

4人のプレーヤーが居た場合、このようにして
今（訳補：このマシンで）制御しているインスタンス、
別の言い方をすると local に生成したインスタンスだけを（訳補：このマシンのボタンで）動かします。

残りの3つのインスタンスについては、
``self.pressed_jump`` などの変数は他の3人のプレーヤーによって変更されます。

（訳注：この残りの3つのインスタンスでの、
ネットワーク越しに送られてきた情報による変数の変更は、
すでに ``end step`` に追加した ``mp_map_syncOut`` 関数呼び出しの行で行われます。）

**プレーヤー1の視点で描いた次の表を見てください**

| インスタンスは    | ボタンで制御されるか | エンジンで制御されるか             |
| ----------------- | -------------------- | ---------------------------------- |
| プレーヤー1のもの | はい                 | いいえ                             |
| プレーヤー2のもの | いいえ               | はい（プレーヤー 2 からのボタンで）|
| プレーヤー3のもの | いいえ               | はい（プレーヤー 3 からのボタンで）|
| プレーヤー4のもの | いいえ               | はい（プレーヤー 4 からのボタンで）|


（訳注：
（この訳注の考察が正しいのか裏をまだとっていません。TODO 確認する。）

このデモプログラムでは、
ローカル生成インスタンスとリモート生成インスタンスとで、
制御変数の書き換えとそれを使った計算のタイミングが若干ずれます。
コードの動きをその違いに着目して書き出すと次のようになります。
（表の下向きに時間が流れるものとして書いています。）

| event     | local インスタンスの動作                    | remote インスタンスの動作 |
|-----------|---------------------------------------------|----------------------|
|begin step | keyboard_check で取り込み, syncInで書き出し | （実質何も起きない） |
|step       | pressed_jump など元に速度や座標を計算       | ←同じ               |
|end step   | （実質何も起きない）                        | syncOut で取り込み   |

この後 ``draw event`` が起きると

| event     | local                                        | remote               |
|-----------|----------------------------------------------|----------------------|
|draw       | 速度や座標は pressed_jump などを反映している | まだ反映していない   |

という違いがおきます。
remote の場合の演算は次の step で行われ、両者はそこで同じ状態になります。

したがって、
「このようにプログラムを組んで draw などで計算結果を利用する場合には、
計算結果と同期させている変数の両方を使ってはいけない」
という注意事項が導かれます。
例えば、``pressed_jump`` を draw で使うのなら、
step でさらに別の変数に移し変えるようにする必要があるでしょう。

もっともこれは GMnet 利用に限った事ではなく、
[リファレンスの Events 中 Event Order 節](http://docs.yoyogames.com/source/dadiospice/000_using%20gamemaker/events/index.html)
に書かれているように GML でのイベントの処理順は定義されないので、
「イベントの順番に依存せずに内部状態を書き換え、参照する」という一般的注意の一例だといえます。）

###テスト
ゲーム・プログラムを二つ起動し、
一つはゲーム・サーバを選択し、
もう一つはクライアントとして 127.0.0.1 に接続します。

二人のプレーヤーがあらわれ、
**マルチプレーヤーアクションゲームが完成しているでしょう**。

（訳注：冒頭に書かれていたように、基礎部分の解説はこの項までで終わりました。
残りの部分は発展的な話題です。）


---
##7. Adding a player

Okay, okay, I know we already added a player in Step 5.

    ??? How about making a link as [in Step 5](tutorial/5_platformer) ?

What this title means, is simply that we are now **adding the player to the engine**. After this step the player will be **synchronized between all players you connect to your server**.  
So we are basicly done after this step. The rest of the tutorial is some more advanced stuff.

###The create event

To set the player up, we only have to make minimal adjustments. **Create a new code block in the create event**, and insert it **before** the other block.

Start the code block with 
```gml
mp_sync();
```

This will **tell the engine to sync this object**. Once this was created on one client, this instance wil also be **sent to all other players**. 

    ??? "instance wil"
    ??? "wil" => "will"

    ??? "This will"..."Once this was"..."this instance"
    ??? I think there's too many "this" and thease are little bit ambiguous.
    ??? The first "this" points the code "mp_sync()".
    ??? Does the second "this" points newly created object instance?

If you add one player instance to your room and connect 4 players togther, each player will have four player instances.

Now we need to tell the engine what variables to sync and how:

```gml
mp_addPosition("Pos",5*room_speed);
```

This will tell the engine to sync the position variables ``x`` and ``y`` every 5 seconds. ``5*room_speed`` means 5 seconds. The first argument of ``mp_addPosition`` is the name of group. You can choose that however you want.

What we just added is a so called **variable group**. The group is called "Pos", get's synced every 5 seconds and sync the variables ``x`` and ``y``.

    ??? "is a so called" .. "group is called"
    ??? Too close two "called"
    ??? How about : The name of the group is "Pos" and the group is synced ...

Let's set **how the position should be synced**:

```gml
mp_setType("Pos",mp_type.SMART);
```

This changes the **sync type** to the variable group "Pos". **The default sync type is FAST**. We are changing it to **SMART**. Here is a list of what every sync type does:

    ??? "the **sync type** to the variable group"
    ??? I suggest to replace "to" with "of"

* **FAST** (default, you don't have to use ``mp_setType`` if you want to use that):
  In our case, if we had chosen FAST, the engine would send the position of our player every 5 seoncds **once**. Since we are using UDP for networking, there is no assurance, that it will actually arrive. That means we don't know if the other players actually get our position every 5 seoncds. The packet could get lost. However, using FAST is very... FAST. You will see when we want to use FAST later in this section.
* **IMPORTANT**:
  When using IMPORTANT, in our case the position would still be synced every 5 seoncds. However, we are using a special way in *GMnet ENGINE* to make sure the packet arrives. Every 5 seconds, the server/client will flood the other players with the information, until they respond back, that they got it. That's how we assure the information is actually sent. This is however a pretty traffic heavy operation and using that in too short intervals will cause lagg in both connection and framerate.

    ??? typo? "lagg" => "lag"

* **SMART**:
  This is like IMPORTANT but better. Instead of syncing every 5 seconds, we will only sync every 5 seconds what has changed. If only the x position changed, we are not syncing the y position. If our position has not changed at all, we are not syncing. This is basicly a more traffic-friendly version of IMPORTANT.

We are using **SMART** here and relatively large intervals, because we only sync the position as a backup. As you will see later, we are going to sync the button inputs every single step. **We only sync the position to make sure, the players don't get desynchronized**.

The** button input later will be synced FAST**. That means **some packets could be lost**, and after some time the player could be on two completly different parts of the level, depending on the complexity of your platformer. To make sure that doesn't happen, **we reset the position every 5 seconds**.

Now, the thing is, if we reset it every 5 seconds, it might happen that **the players are just some pixels off**. In that case our players might **slightly "flicker"** whenever the position resets. **That doesn't look nice**.

Let's add a little **tolerance range**. If the position at is **less than 20 pixels away from where it should be**, the other players should **not apply this change** locally, so it **doesn't flicker** that much:

```gml
mp_tolerance("Pos",20);
```

Great. Position is set up. Now, **just to make sure**, let's also sync **the basic Game Maker physics and drawing variable**s:

```gml
/**
 * Tell the engine to add the basic drawing variables:
 * image_alpha,image_angle,image_blend,image_index,image_speed,image_xscale
 * image_yscale,visible
 */
mp_addBuiltinBasic("basicDrawing",15*room_speed);
mp_setType("basicDrawing",mp_type.SMART);

/**
 * Tell the engine to add the builtin GameMaker variables:
 * direction,gravity,gravity_direction,friction,hspeed,vspeed
 */
mp_addBuiltinPhysics("basicPhysics",15*room_speed);
mp_setType("basicPhysics",mp_type.SMART);
```

We don't need to sync them that frequently. If we sync physics to frequently that might look weird and we are only syncing the basic Drawing stuff for the player color (``image_blend``) which doesn't change anyway, and the ``image_xscale`` and ``iamge_angle`` which controls how the player faces, which isn't that critical.

Now we also want to **sync the name**:
```gml
mp_add("playerName","name",buffer_string,60*room_speed);
mp_setType("playerName",mp_type.SMART);
```

This is using ``mp_add`` to sync our own variables. The syntax is slightly more compelx and we need to do some things to make this work later, but let's just see what we got here:
* The first argument is again the name of the group
* In the second argument you specify the **names of the variables** you want to sync, **seperated by commas**. We stored the player name in the "name" variable.
* The third argument is the **buffer type**. You can find information on which buffer type you need to use on [this manual page](concepts/buffer). **All variables need to have the same buffer type.** ``buffer_string`` simply means that the variable "name" stores a string.
* The last argument is the syncing interval, just as before.

We decide for a 60 seconds interval, because the name will never change. We could have also used 20 years, that wouldn't make a difference. We only need to make sure the engine syncs it on login and some other critical events, and it does that automatically, no matter what interval we choose. We still need to make it SMART because we need to make sure it REALLY arrived at those events.

Next up are the **controls**. Remember how we stored the button input in seperate variables? Well now you might know why:

```gml
mp_add("controls","pressed_jump,pressed_left,pressed_right",buffer_bool,1);
```

The "buffer type" is ``buffer_bool``, because our "pressed\_" variables are booleans. 1/0, true/false.

This will **sync the button input to all players every single frame** no matter what. We don't want to have it SMART or IMPORTANT. **FAST is the way to go**, since there is **no point in checking if the data arrives**, because we are syncing the button input every step anyway.


###Some things needed when using ``mp_add``

Since we are using ``mp_add`` to sync our own variables, we need to make some code changes. We need to send the variables to the engine at the beginning of the step, and retrieve the data at the end.  
The reason fot that is, that in Game Maker there is [no way of getting a variable's content by accessing it via a string](http://gmc.yoyogames.com/index.php?showtopic=646036&hl=). We need to store the values to a map first before the engine can read them. This is not needed for ``mp_addPosition``, ``mp_addBuiltinBasic`` and ``mp_addBuiltinPhysics``, because we hardcoded them.

    ??? "The reason fot that is"
    ??? typo? "fot" => "for"

    ??? "We need to store the values to a map first before the engine can read them"
    ??? I think it's better not to refer to "map",
    ??? because that map object is a matter of GMnet internal implementation.
    ??? How about just say "store to engine" ?

If you don't know what any of that means what I just said, don't worry. It's complicated.

**The only things you need to know, we will explain them now:**

For every object where you use ``mp_add`` add the following to the **begin step** event:

```gml
mp_map_syncIn("name",self.name);
mp_map_syncIn("pressed_jump",self.pressed_jump);
mp_map_syncIn("pressed_left",self.pressed_left);
mp_map_syncIn("pressed_right",self.pressed_right);
```

Replace the names with the names of your synced variables. These are the variables that we created above for our tutorial player.

    ??? "tutorial player"
    ??? In some parts of this tutorial, it refers the program as "demo", while here refers as "tutorial".
    ??? I think that is little bit confusing for readers.

All changes to these variables need to be made **BEFORE** using these functions. That means you either have to change them in begin step, or call ``mp_map_syncIn`` again after you changed variables. We recommend the first. And that's also what we are going to do in a minute.

In the **end step** event add the following code to retrieve the variables again:

```gml
self.name = mp_map_syncOut("name", self.name);
self.pressed_jump = mp_map_syncOut("pressed_jump", self.pressed_jump);
self.pressed_left = mp_map_syncOut("pressed_left", self.pressed_left);
self.pressed_right = mp_map_syncOut("pressed_right", self.pressed_right);
```

###Setting up controls for synchonization

Last thing we need to do, is to **move this code out of the step event** we created earlier:
```gml
self.pressed_jump = keyboard_check(vk_space);
self.pressed_left = keyboard_check(vk_left);
self.pressed_right = keyboard_check(vk_right);
```

**Simply remove it**. In begin step, **add the following code** **before** the other code:

```gml
if (htme_isLocal()) {
    self.pressed_jump = keyboard_check(vk_space);
    self.pressed_left = keyboard_check(vk_left);
    self.pressed_right = keyboard_check(vk_right);
}
```

It should now look like this:

```gml
if (htme_isLocal()) {
    self.pressed_jump = keyboard_check(vk_space);
    self.pressed_left = keyboard_check(vk_left);
    self.pressed_right = keyboard_check(vk_right);
}
mp_map_syncIn("name",self.name);
mp_map_syncIn("pressed_jump",self.pressed_jump);
mp_map_syncIn("pressed_left",self.pressed_left);
mp_map_syncIn("pressed_right",self.pressed_right);
```

All the code we just pasted in begin step does, is **check if this is the instance that was locally created** and then **writes the button input of the players into the variables**.

This way when we have 4 players, we only move the instance we control, the instance we locally created. The ``self.pressed_jump...`` variables will be changed by the other 3 players for the rest of the three instances.

**Look at the following table from the view of player 1:**

| Instance/Player | Controlled via buttons | Controlled via engine      |
| --------------- | ---------------------- | -------------------------- |
| Ours / Player 1 | Yes                    | No                         |
| Player 2'   s   | No                     | Yes, buttons from Player 2 |
| Player 3'   s   | No                     | Yes, buttons from Player 3 |
| Player 4'   s   | No                     | Yes, buttons from Player 4 |

###Test
Fire up two games and create a server / connect to 127.0.0.1.

You should now see both players, **and should see that we now have a multiplayer platformer.**

---

**» Next topic: [A second room and doors](tutorial/8_doors)**

« Previous topic: [The network controller](tutorial/6_networkcontroller)
