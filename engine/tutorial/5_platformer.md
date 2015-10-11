##5. 基本的な platformer（訳注：ジャンプ・アクション・ゲームの機能）を整える

（訳補：マルチプレイについて示す前に）まずはシンプルな platformer を作る必要があります。
** これは platformer 作成のチュートリアルはない ** し、
ここで使うのはシンプルでちょっとばかり（訳補：出来が）悪いものなので、
単に説明を通し見てコードをコピーしてください。

###1. game room を整える

先の手順で作った game room ``htme_rom_demo`` に素敵な **background color** を設定し、
大きさを **800x600** にします。
このデモでは view 機能は使いません。

###2. 壁を作る

solid object を新規作成して ``htme_obj_wall`` と名づけます。
sprite に ``htme_spr_wall`` を設定します。
（訳注：チュートリアル冒頭で sprite を インポートしていればプロジェクトに含まれているはずです。）
（訳注：緑色の四角ではありますが）これがこのゲームでの「壁」です。
game room に配置して、壁や床やプラットフォーム（訳注：高いところに水平に配置した台）など作ってください。


###3. プレーヤー object を作る

次にプレーヤーを作ります。

新しい object を作り ``htme_obj_player`` と名づけ、sprite に ``htme_spr_player`` を設定します。

**create-Event** に次のコードを書きます：

```gml
///Setup basic stuff for the demo platformer.
self.pressed_jump = false;
self.pressed_left = false;
self.pressed_right = false;
self.name = "";

/** Totro generates random names and is not part of the main engine, it's
  * another marketplace asset by me :)
  */
var ttr = totro(5,7,1);
self.name = ttr[0];
/** Gives this player a random color. */
self.image_blend = irandom(16777215);
}
```

（訳注：次は中ほどの totro 関数についての説明。）
（注： Totro はランダムな名前を生成するもので、エンジンの一部ではありません。。
marketplace に登録してある私（訳注：原著者のこと）の別の asset です。）
（訳注：totro 関数は GMnet ENGINE のデモ部分として Scripts/htme_demo/totro として収められています。
全ての Scripts を取り込んでいれば使用できるはずです。）


``self.pressed`` で始まる変数群は移動やジャンプのためのボタンを押したかどうかを保持します。
後でプレーヤをエンジンに登録する際に必要になるので、
ここで準備として保持しておく必要があります。（訳補：詳しくは）後ほど見ます。

**step event** に次のコードを書きます：

```gml
///Perform platforming!
//This is a very basic example of a platformer. You should not program your physics like this!

if (place_free(x, y+1)) {
   gravity = 0.2;
} else {
   gravity = 0;
   vspeed = 0;
}

self.pressed_jump = keyboard_check(vk_space);
self.pressed_left = keyboard_check(vk_left);
self.pressed_right = keyboard_check(vk_right);

if (self.pressed_jump && (!vspeed)) {
    vspeed = -12
    image_xscale = 1;
    image_angle = 90;
}
if (self.pressed_right) {
    x+=10;
    image_xscale = 1;
    image_angle = 0;
}
if (self.pressed_left) {
    x-=10;
    image_xscale = -1;
    image_angle = 0;
}
if (vspeed < 0) vspeed=vspeed+gravity;
```

（訳：これはごく基本的な platformer です。物理演算をこんな風にプログラムしちゃ駄目です！）

見れば分かるように、
ここではボタンのプレス状態を ``self.pressed`` 変数群に保存してチェックしています。
これは後ほど変更します。


次に **htme_obj_wall との Collision event** を作り、次のコードを書きます：

```gml
///Set speed to 0 when hitting a top wall
if (!place_free(x, y-16)) {
    move_contact_solid(90,-1);
    vspeed = 0;
}

if (!place_free(x, y+16)) {
   move_contact_solid(270,-1);
   gravity = 0;
   vspeed = 0;
}
```

最後に **draw event** で、
create event で作ったランダムな名前を描画するコードを書きます。
action に **draw self** を置き、その次にこのコードを書きます：

```gml
///Draw nameplate
draw_set_color(image_blend);
draw_set_halign(fa_center);
draw_text(x,y-sprite_yoffset-5-string_height(self.name),self.name);
draw_set_halign(fa_left);
draw_set_color(c_white);
```

基本 platformer：完了！

###4. テスト

プログラムを開始してゲーム・サーバーを開始します。
するとこの platformer がどれだけひどいかテストできます。
でもでも、動くでしょ。
次のチュートリアルが実際にエンジンに再度関係する部分です。


---
##5. Setting up the basic platformer

We now need to create a simple platformer. Since **this is not supposed to be a tutorial on platformers**, and the platformer we are going to use is simple and pretty bad, simply follow the instructions and copy the code.

###1. Setup our game room

Give the game room ``htme_rom_demo`` we created a nice **background color** and the dimensions **800x600**. For this demo, we are not going to use views.

###2. Create a wall

Create a solid object, called ``htme_obj_wall``. Give it the sprite ``htme_spr_wall``. This is our new wall. Place it into the game room, build some walls, a floor and maybe some platforms.

###3. Create the player object

Next we are going to create our player.

Create the object ``htme_obj_player`` and give it the sprite ``htme_spr_player``.

Into the **create-Event** put the following code:

```gml
///Setup basic stuff for the demo platformer.
self.pressed_jump = false;
self.pressed_left = false;
self.pressed_right = false;
self.name = "";

/** Totro generates random names and is not part of the main engine, it's
  * another marketplace asset by me :)
  */
var ttr = totro(5,7,1);
self.name = ttr[0];
/** Gives this player a random color. */
self.image_blend = irandom(16777215);
}
```

The ``self.pressed...`` variables will store if our player pressed the buttons to move or to jump. We need to store this in a variable as a preperation for later, when we want to add the player to the engine. But you'll see :).

Into the **step event** put the following code:

```gml
///Perform platforming!
//This is a very basic example of a platformer. You should not program your physics like this!

if (place_free(x, y+1)) {
   gravity = 0.2;
} else {
   gravity = 0;
   vspeed = 0;
}

self.pressed_jump = keyboard_check(vk_space);
self.pressed_left = keyboard_check(vk_left);
self.pressed_right = keyboard_check(vk_right);

if (self.pressed_jump && (!vspeed)) {
    vspeed = -12
    image_xscale = 1;
    image_angle = 90;
}
if (self.pressed_right) {
    x+=10;
    image_xscale = 1;
    image_angle = 0;
}
if (self.pressed_left) {
    x-=10;
    image_xscale = -1;
    image_angle = 0;
}
if (vspeed < 0) vspeed=vspeed+gravity;
```

As you can see, we currently just put the button presses into the variables ``self.pressed...`` and check them. We will change that later.

Now create a **Collision with htme_obj_wall event** and put the following code in it:

```gml
///Set speed to 0 when hitting a top wall
if (!place_free(x, y-16)) {
    move_contact_solid(90,-1);
    vspeed = 0;
}

if (!place_free(x, y+16)) {
   move_contact_solid(270,-1);
   gravity = 0;
   vspeed = 0;
}
```

Into the **draw event**, we will put some code to draw the name we randomly generated in the create event. First put "**draw self**"" into the event and then this code:

```gml
///Draw nameplate
draw_set_color(image_blend);
draw_set_halign(fa_center);
draw_text(x,y-sprite_yoffset-5-string_height(self.name),self.name);
draw_set_halign(fa_left);
draw_set_color(c_white);
```

Basic platformer: Done!

###4. Test

Start the game and then start the server. You can now test out how bad the platformer really is. But hey, it does the job. The next tutorial is actually related to the engine again.

![How it should look like](images/1.PNG)

    ??? Where is the image file?
    ??? No image file in this repository
    ??? even at the site ( http://gmnet.parakoopa.de/manual/engine/tutorial/5_platformer)

---

**» Next topic: **[The network controller](tutorial/6_networkcontroller)**

« Previous topic: [Starting the engine](tutorial/4_starting)
