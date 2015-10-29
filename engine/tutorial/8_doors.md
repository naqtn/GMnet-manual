##8. 二番目の room とドア

これで、簡単なマルチプレーヤーゲームを作るのに必要なほとんど全てのことは知ったことになります。

以降の節は以下のより発展的な話題を使います。といっても、とても難しいということはありません。

* 複数の room と共にマルチ・プレーヤー・エンジンを使用する
* マルチ・プレーヤー・エンジンのデータの操作

まず**二番目の room を作り**ましょう。
単純に ``htme_rom_demo`` を **コピー** して（訳補：``htme_rom_demo2`` と命名し）、壁の配置を少し変えます。
背景色も変えると良いでしょう。
**room から壁と ``htme_obj_network_controller`` 以外の全ての object を取り除きます。**

この room にプレーヤーを入らせるには、次の二つの（訳補：問題解決）アプローチがあります。

1. ``htme_rom_demo2`` に新たなプレーヤー・インスタンスを置く。プレーヤー object は persistent にはしない。
2. プレーヤーインスタンスを persistent にする。
  Game Maker では persistent object （訳注：persistentを有効に設定した object）は
  room を変更した後も存在し続ける。

（訳注：persistent （日：永続的な、パーシステント、常に存在し続ける）は、
GMS の object 編集のウィンドウでチェックボックス操作して設定します。）

このチュートリアルでは**二番目の**アプローチを使います。
その理由は、persistent object と（訳補：その）インスタンスがどのように振舞うかも説明したいからです。
しかし（訳補：説明したいということを別にしても）もし一番目の方法でゲームを作れるのであれば、
多くの場合、二番目のアプローチも同様に機能するでしょう。
お勧めは、二番目のアプローチです。


（訳補：というわけで）
**``htme_obj_player`` を persistent に設定します**。
プレーヤを次の room に移動するようにするのに
プレーヤー object について必要なこと（訳注：変更内容）はこれで全てです。

次に``htme_obj_door`` **object を作り** スプライトに ``htme_spr_door`` を設定します。
（訳注：このスプライトは GMnet の配布物に添付されています。）

**``htme_obj_player`` との衝突 collsion （日：衝突、コリジョン）イベントを作成** して、
（訳注：そのアクションとして）次のコードを追加します：

```gml
///CHECK IF DOOR ENTERED
var isLocal;
with (other) {isLocal = htme_isLocal();}

if (isLocal && keyboard_check_pressed(vk_up)) {
    var dest = htme_rom_demo2;
    if (room == htme_rom_demo2) dest = htme_rom_demo;
    room_goto(dest);
}
```
（訳：ドアに入ったかどうか検査）

これはプレーヤーがドアの前に立っている時に、
other インスタンス（これは（訳補：このドアと衝突した） ``htme_obj_player`` object のインスタンス）が
ローカルのプレーヤーかどうかを（ローカル変数 ``isLocal`` に情報を保存しつつ）判定します。

（訳注：ドアと衝突したプレーヤー・インスタンスが、
GMnet の同期機構によって他からコピーされてきたものではなく、
このマシンでユーザーが操作しているプレーヤー・インスタンスかどうかの検査をする、
ということです。）

ローカルのプレーヤー（訳注：つまり操作しているキャラクタ）だった場合、room を変更します。
room は現在の room によって ``htme_rom_demo`` と ``htme_rom_demo2`` を相互に変更します。
**ドアはそれぞれの room に配置します。**


**これで終わりです。**

クライアントとサーバーを開始し room を変更してみてください。
あなたが期待するように動作するでしょう。
もし動かないのであれば、
プレーヤー object を persistent に設定しているか、
ドアを両方の room で同じ位置に置いているかを確認してください。

（訳注：この実装では room を変更するだけでプレーヤーの座標はそのままなので、
それらしく見せるためにドアはそれぞれの room で同じ座標位置に配置しておく必要があります。）


###技術上の話を少々

persistent な object を作るとローカルでのみ persistent になります。

つまり、他のプレーヤーが room を変更すると、
あなたのゲームの中では（訳補：そのプレーヤーのインスタンスは）存在しなくなります。
その room にあなたが入ると、あなたのクライアントに
（訳補：そのプレーヤーの情報は）再度送信され、再生成されます。

表にまとめると次のようになります。
**A によって room 1 で作られたインスタンスについて：**

![表（画像ファイル）](../images/2v2.PNG)

後ほど、
全てのプレーヤーに対してインスタンスが常に見える（存在する）ようにする三番目の筋書き（シナリオ）を導入し、
この表を拡張します。


（訳注：この表は、
二人のプレーヤー（A, B）が接続している場合に、
object の persistent の設定状況（縦軸）と、
それぞれのプレーヤがどちらの room に今居るか（横軸）の組み合わせで、
A によって room 1 で作られたインスタンスがそれぞれのプレーヤーから見えるかどうかを書いた表。

「Vis. for A?」は 「A から見えるか？」で「×」の欄が「見えている」を意味している。
（日本の文化では丸を描くところだろうが、原著者は「該当する」のチェックの意味で印を書いている。）

表を横にたどって見ていくと、
persistent ではない場合には
A にとっては元の room 1 だけで存在していて、2 に移動すると見えない。
B にとっては A と一緒に room 1 にいる時にのみ見える。

persistent にすると、
A にとっては room を移動しても存在し続けるようになる。
ただし B にとってはやはり A と一緒の room にいるときにのみ見える。
つまり B にとっては persistent ではなく、
「ローカルでのみ persistent」とはこのことを意味している。
）


---
##8. A second room and doors

Now you know nearly everything needed to make a very simple multiplayer game. 

The next sections will cover the following more advanced, but still not very difficult, topics:

    ??? next ? "from here"?

* Using the multiplayer engine with mutliple rooms
* Working with the data of the multiplayer engine

We are now going to **create a second room**. Simply** copy** ``htme_rom_demo`` and restructure the walls a bit. Maybe you could also change the background color. **Remove all other objects from the room, except the walls and ``htme_obj_network_controller``.**

There are two aproaches you could use if you want the player to enter this room:

1. Place a new player instance in ``htme_rom_demo2``, make the player object NOT persistent
2. Make the player instance persistent; Persistent objects in Game Maker exist even after you change the room.

For this tutorial we are using the **second approach**. The reason for that, is that we also want to teach you, how persistent objects work with the instance. But if you solve your game using the first method, this should also work in most cases. Please note that the second approach is recommend though.

**Make your ``htme_obj_player`` persistent**. That's all we need to do in the player object if we want him to move to a second room.

Now **create the object** ``htme_obj_door`` with the sprite``htme_spr_door``.

Create a **Collsion with ``htme_obj_player`` event** and add this code:

```gml
///CHECK IF DOOR ENTERED
var isLocal;
with (other) {isLocal = htme_isLocal();}

if (isLocal && keyboard_check_pressed(vk_up)) {
    var dest = htme_rom_demo2;
    if (room == htme_rom_demo2) dest = htme_rom_demo;
    room_goto(dest);
}
```

This checks when a player is standing in front of a door if the other instance, which is an instance of the object ``htme_obj_player`` is our local player by storing this information in the local variable ``isLocal``. When it's our local player ("we") we change the room. The room is changed to ``htme_rom_demo2`` when in ``htme_rom_demo`` and viceversa. **Place a door in each room**.

**We are done.**

Now start a client and server again and try switching rooms. Everything should work as you would expect it. If not, check again if you made the player object persistent and make sure the doors are on the same position in both rooms.

###Some technical stuff

When you make persistent objects, they are only persistent locally.

That means when another player switches room, they will cease to exist in your game. When you enter the room they will be resent and recreated to your client.

Here is a nice little table **FOR AN INSTANCE CREATED BY A IN ROOM 1**:

![The table](images/2v2.PNG)

We will extend this table later with a third scenrio that makes the instances visible/existent at all time for all players.

    ??? typo "scenrio" => "scenario"

---

**» Next topic: [Making an overlay that shows the name of connected players](tutorial/9_playerlist)**

« Previous topic: [Adding a player](tutorial/7_player)
 
