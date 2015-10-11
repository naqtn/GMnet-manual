##3. **PLUS** - マスターサーバー (GMnet GATE.PUNCH) の設置

*GMnet PUNCH* の魔法を使うには 仲介/マスター/ランデブー （訳注：同じ物を異なった表現で言い換えている）
サーバーを設置する必要があります。

このサーバーは Java 言語で書かれた小さなアプリケーションで、
** フォワードないしはオープンされたポート ** が必要です。

何故これが必要となるかを説明するために、
ホール・パンチングがどのようにして動くかを説明させてください：

* ゲーム・サーバはマスター・サーバー（GMnet GATE.PUNCH）に接続し、ポート番号とIPアドレスを登録する。
* クライアントがゲーム・サーバに接続したい時には、自身のポート番号とIPアドレスを（訳補：マスター・サーバーに）登録し、ゲーム・サーバに送る。そしてサーバーのポート番号とIPアドレスを受け取る。
* これで双方が UDP パケットを同時に送りあえる。つまりホールがパンチされたことになる（訳注：穴が開けられた）。


クライアントが接続したいという事をゲーム・サーバーに気づかさせるために
マスターサーバー（GMnet GATE.PUNCH）が必要です。


次の場所から（訳補：GMnet GATE.PUNCH は）ダウンロードできる：

http://gmnet.parakoopa.de/gatepunch

このサーバはとても基礎的なものなので、必要に応じて自由に変更してください。

現在のところ、このサーバの実行形式は ** ポート 6510 ** を使います。
サーバーのソースをコンパイルしたくないのであればそこを使うことになりますが、
将来には（訳補：ポートを指定できる）オプションを付け加えるつもりです。



サーバをスタートするには：

サーバを保存したフォルダで
``java -jar gmnet_gate_punch.jar``
を（訳補：コマンドラインで）実行します。

Windows では``java`` を Java のフルパスに置き換える必要があるかもしれません。
（訳注：標準設定では "c:\Program Files\Java\jre1.8.0_51\bin\java.exe" などの場所にインストールされます。）
Linux でバックグラウンドで実行させるには ``screen`` を使うのをお勧めします。


### ホスティング（サーバの設置）

安価なホスティングサービスとして個人的には **digitalocean** をお勧めします。 
サーバー（訳補：の価格）は一時間当たり $0.0015（月に5ドル）からでいつでもキャンセルできます。

Java をセットアップするチュートリアルもあります。
promo code をググれば２ヶ月無料になります。（訳注：販売促進のためのクーポンのようなもの）
基本的には Linux サーバへの完全なアクセスを提供しています。

digitalocean を使いたいと思うのなら、どうぞ次のコードで登録してください：
https://www.digitalocean.com/?refcode=1bff6d6dff1a



（訳注：以下 digitalocean の使い方なので、一旦翻訳保留。）


#### Some tutorials:

If you want to know how to login to the server:
https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet-virtual-server

For some basic commands and stuff:
https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-basics

If you want to install java:
https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get

For transfering the master server:
https://www.digitalocean.com/community/tutorials/how-to-use-filezilla-to-transfer-and-manage-files-securely-on-your-vps
[You can skip the stuff with the keyfile and everything. Simply install filezilla and connect to sftp://yourip with your username and password]

When you are done simply execute ``java -jar gmnet_gate_punch.jar``

As I said, I recommend install screen, it allows you to run commands even if you are not logged in, running in the background and you can just switch to them at any time:
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-screen-on-an-ubuntu-cloud-server


---
##3. **PLUS** - Hosting a master server (GMnet GATE.PUNCH)

To use the magic of *GMnet PUNCH* you need to host a mediation/master/rendevouz server. The server is a small application written in Java that needs to be run on a server **with a forwarded/open port**.

To explain why you need this, let me explain how the hole punching works:
* The server connects with the master server (GMnet GATE.PUNCH) and its port and ip get registered.
* When the clients want to connect to this server, his port and ip also get registered and sent to the server. And the client gets the ip and port of the server.
* Now both send UDP packets to each other at the same time: The hole is punched.

We need the master server (GMnet GATE.PUNCH) because we need to make the server aware of the fact that a client wants to connect.

The download can be found here:

http://gmnet.parakoopa.de/gatepunch

The server is very basic, feel free to adjust it to your needs.

Currently the server binary listens on **port 6510** and there to change it if you don't want to compile the server yourself, but we will add that option in the future.

     ??? "and there to change"
     ??? cant get meaning.

To start it, run:
``java -jar gmnet_gate_punch.jar``
from the folder you saved the server in. Under Windows you might need to replace ``java`` with the full installation path of java. Under linux I recommend ``screen`` to run it in the background on a server.

###Hosting

For cheap hosting I personally recommend **digitalocean**. Server start at $0.0015 per hour (5$ per month) and you can cancel at every time.

Google yourself a promo code and you might get two months for free. There are also tutorial on how to set up java on these servers. They are basically linux servers with complete access.

If you want to use digitalocean, please use this code to register:
https://www.digitalocean.com/?refcode=1bff6d6dff1a

####Some tutorials:

If you want to know how to login to the server:
https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet-virtual-server

For some basic commands and stuff:
https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-basics

If you want to install java:
https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get

For transfering the master server:
https://www.digitalocean.com/community/tutorials/how-to-use-filezilla-to-transfer-and-manage-files-securely-on-your-vps
[You can skip the stuff with the keyfile and everything. Simply install filezilla and connect to sftp://yourip with your username and password]

When you are done simply execute ``java -jar gmnet_gate_punch.jar``

As I said, I recommend install screen, it allows you to run commands even if you are not logged in, running in the background and you can just switch to them at any time:
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-screen-on-an-ubuntu-cloud-server


---

**» Next topic: [Starting the engine](tutorial/4_starting)**

« Previous topic: [**PLUS** - Setup GMnet PUNCH](tutorial/2_udphp1)
