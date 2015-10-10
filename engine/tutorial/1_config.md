##1. 基本設定

このチュートリアルでは **シンプルなプラットフォームゲーム** （訳注：ジャンプアクションゲーム）に
*GMnet ENGINE* が出来る事をデモンストレーションするイカしたちょっとした要素を追加したものを
作ろうと思います。

このゲームには次のものを含めようと思います：

* 壁/プレーヤー/物理 （これは当然ですね）
* 複数の面（room）
* 接続されているプレーヤーを表示するオーバーレイ
* 昼夜の周期
* 基本的なチャットシステム


### エンジンをプロジェクトに追加する

始める前に、
アセット（asset）を空のプロジェクトに加えます。
何をしたいかによって、３つの選択肢があります。

* もし **このチュートリアルにしたがって実際に作業を進める** のならば、 ** 全ての scripts と sprites それから ``obj_htme`` object ** をプロジェクトに追加する。
* ただ **チュートリアルを読み通し** てデモゲームを試すだけなら、**ただ全部を追加する**。
* 完全に空のプロジェクトから始める、もしくは **あなたのゲームにエンジンを追加する** のであれば、
全ての ** *htme* フォルダ ** と ** *udphp* フォルダ ** を追加する（**not the *htme_demo* folders** は不用）。（訳注：htme, udphp フォルダは複数のリソースの下にあるのでそれら全て）


### 設定

すばらしい！
どの選択肢を選んだ場合でも、おそらく設定について確認したいでしょう。説明していきましょう。

** 設定は ``scripts/htme/htme_init`` にあります **。
この設定の最初部分はエンジンが使う列挙（enum）です。
それは無視して ``CONFIGURATION`` に進みましょう。
（訳注：その先の方にコメントで CONFIGURATION と書いてある部分のこと）

CONFIGURATION の下に最初に見つかるのは ``randomize();`` です。
これは Game Maker の乱数操作が正しく乱数になることを保証しています。
これはエンジンにとって重要です。

その次で **debug level** が設定できます。
設定できる値は ``htme_debug`` 列挙にあります。（訳注：少し上に htme_debug の定義がある）
どのように働くかはここのコメントに書いてあります。
今はデフォルトのままにしておきましょう。

その先の **``self.global_timeout``** までは読み飛ばしましょう。

この ``self.global_timeout`` は実際のところ唯一の重要な設定項目です。デフォルトのままにしておいても構いません。

タイムアウトは何ステップの不活性後に、
クライアント・サーバ間の接続が死んで切断されるかを指定します。

デフォルトは ``5*room_speed`` で、これは基本的に５秒を意味します。
クライアントとサーバが互いに5秒通信しなければ、接続していないと見なします。

うん！今のところ設定するのはこれだけです。

設定の次のステップでは、
GMnet ENGINE（正確には GMnet PUNCH）が
ファイヤーウォールの中からでも他のプレーヤーと接続できるようにすることを説明します。

---

##1. Basic configuration

In this tutorial we want to make a **simple platformer** with some neat little extras to demonstrate what *GMnet ENGINE* can do.
Our platformer will have:

* Walls/Players/Physics (obviously)
* Multiple rooms
* An overlay that shows connected players
* A night and day cycle
* A basic chat system

###Adding the engine to a project
Before we can get started, add the asset to an empty project. Depending on what you want to do, you have three options.

??? "an empty project"
??? For "add the engine to your own game" case, it's not empty.
??? So I suggest removing "empty"
 
* If you want to **follow this tutorial yourself**, you should add **ALL scripts and sprites and the object ``obj_htme``** to your project.  
* If you want to just **read through this tutorial** and test the demo game, **simply add everything**. 
* When starting completely blank or when you want to **add the engine to your own game**, add all **folders named *htme*** and ***udphp*** but **not the *htme_demo* folders**.

###Configuration
Great! No matter what option you chose, you propably want to take a look at the configuration, so let me walk you through.

??? propably
??? misspell of "probably"?

**The configuration can be found in ``scripts/htme/htme_init``**. The first things in this configurations are the enums that are used by the engine. Just ignore them and jump straight to ``CONFIGURATION``.

The first thing you'll find under configuration is ``randomize();``. That assures that the random operations Game Maker does are truly random, which is important for the engine.

After that you can set the **debug level**. Valid options can be found in the enum ``htme_debug`` and how debugging works is explained in the comment. Leave it on the default option for now.

Let's skip ahead to **``self.global_timeout``**. That's actually the only important configuration option and even that can stay on default if you want. Timeout specifies after how many steps of inactivity the connection between client and server will die and you will be disconnected. The default is ``5*room_speed`` which basicly means 5 seconds. When client and server don't communicate to each other for 5 seconds, they are considered to be disconnected.

So yeah that was all there is to configure for now.  

Follow the next steps of the configuration. They will explain how GMnet ENGINE (or GMnet PUNCH to be precise) enables you to connect to other players even behind a firewall.

---

**» Next topic: [PLUS - Setup udphp](tutorial/2_udphp1)**

« Previous topic: [What is GMnet ENGINE?](tutorial/0_whatishtme)
