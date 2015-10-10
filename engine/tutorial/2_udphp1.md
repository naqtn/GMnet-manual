##2. **PLUS** - GMnet PUNCH の設定

望むなら、*GMnet ENGINE* は ** ポート開放しないファイヤーウォールの後ろにいる **
プレイヤーを接続できます。

このためには GMnet ENGINE が必要であることには注意してください。
GMnet CORE を使うだけでは不十分です。

もしあなたが Game Maker Marketplace から GMnet ENGINE をダウンロードしたのなら、
詳しい事をサイトの [version differences](./versiondifferences) で参照すると良いでしょう。

これ（訳補：GMnet PUNCH）を理解するには、誰かと（訳補：オンライン）ゲームをするのであれば、３つの選択肢があるのを知る必要があります。

* プレイ専用サーバ ：多くのシューティングゲーム（訳注：オンライン FPS 等を想定）のように
* サーバへのポートフォワーディング：
  ストラテジゲームやゲーム専用サーバをホストする場合に一般的。（訳注：いわゆるポート開放）
* ホールパンチング -  **GMnet PUNCH** ：GMnet ENGINE に同梱される **GMnet PUNCH** は、UDP ホールパンチを提供します。この技術は、ポートが全くフォワードされていない場合であっても二人のプレイヤーをつなぐことが出来ます。

これは多くの場合動作しますが、必ずというわけではありません。
特にモバイルネットワークやビジネスネットワーク（訳注：つまり一般家庭用ではないルータを介している場合）では失敗することがあります。ホールパンチングはユーザーによってマルチプレイを簡単に行える多くのゲームで使われています。

つまり、 ** *GMnet PUNCH* を無効 ** にすると、あなたのゲームのプレーヤーはオンラインで遊べないか、ローカルだけで遊べるか、あるいはサーバーを立てる必要がある、ということです。

### *GMnet PUNCH* の設定

``htme_init`` script に *GMnet PUNCH* を使うために変更の必要のある変数いくつかあります。

** ``self.use_udphp`` ** : これは最も理解しやすいものです。GMnet PUNCH を有効にするには  **true** に設定します。

** ``self.udphp_master_ip`` ** と ** ``self.udphp_master_port`` ** : あなたの（訳注：あなたのゲームの）仲介サーバの IP と ポート番号。仲介サーバが何なのかは次の節で説明します。基本的には（訳注：仲介のための）サーバを立てる必要があります。（訳注：ゲームの）サーバとクライアントは仲介サーバに接続し、それぞれの情報を共有します。

** ``self.udphp_rctintv`` ** :
どのくらいの頻度（ステップ数）で（訳注：ゲームの）サーバーが仲介サーバに再接続するかを表します。再接続して接続が維持されるされるようにします。ゲームサーバーが仲介サーバに接続されている事は重要なので、大きくしすぎないでください。規定値が適当でしょう。

テスト専用ですが、自分の仲介サーバをまだ持っていないのであれば IP 95.85.63.183 ポート 6510 を使えます。


---
##2. **PLUS** - Setup GMnet PUNCH

If you want *GMnet ENGINE* can be used to connect players **even if the do not forward ports in their firewall**.

    ??? "the do not" > "they"?

Please note, that you need GMnet ENGINE for this, simply using GMnet CORE is not enough. If you downloaded GMnet ENGINE from the Game Maker Marketplace, you are good to go (See the site on [version differences](./versiondifferences) for more information).

To understand this, you need to know, that whenever you want to play a game with someone there are three options:
* Dedicated servers to play on, like most shooters have
* Forwarding a port on the servers firewall, most common when playing strategy games or hosting an own dedicated server of some game
* "Hole-Punching" - **GMnet PUNCH**, which ships with GMnet ENGINE version, allows UDP Hole Punching. This technique allows two players to connect to each other even when no ports are forwarded at all. This works most of the time, however not allways. Especially in mobile networks or buisness networks that might fail. Hole Punching is often used by many games where multiplayer should be easy to do by the user.

That means if you **DISABLE *GMnet PUNCH* **, your players either can't play together online, only locally, or the server has to open ports.

### *GMnet PUNCH* configuration
In ``htme_init`` there are several variables you need to change to use *GMnet PUNCH*.

**``self.use_udphp``**: This is the most obvious one. Set this to **true**, to enable GMnet PUNCH.

**``self.udphp_master_ip``** and **``self.udphp_master_port``**: You need to set these to the ip and the port of your mediation server. What a mediation server is, is explained in the next section. You basically need to host a server, to which server and clients connect to share their information.

**``self.udphp_rctintv``**: How often (in steps) the server should reconnect to the mediation server to make sure it is still connected. It is important that the server is connected to the mediation server, so don't set this too high. The default option should be fine.

If you don't have a server yet you can use the ip 95.85.63.183 and the port 6510 for testing only.

---

**» Next topic: [PLUS - Hosting a mediation server](tutorial/3_udphp2)**

« Previous topic: [Basic configuration](tutorial/1_config)
