#GMnet Manual pages
This is the repository for the manual pages found on http://gmnet.parakoopa.de.  Each manual page is a markdown page. Just like this readme.


**More information about GMnet products can be found on the website:**  
http://gmnet.parakoopa.de


### About this fork ( https://github.com/naqtn/GMnet-manual )

This forked repository is for my Japanese translation trial.

（訳注：この項は原文にはありません。素性を簡単に示すために訳者が記します。）

このリポジトリ https://github.com/naqtn/GMnet-manual は、
https://github.com/Parakoopa/GMnet-manual をフォークしたものです。
日本語訳作成を試みてみます。
冒頭部分は、非日本語話者のために原文をそのまま掲載しました。

GMnet は、[GameMaker: Studio](http://www.yoyogames.com/studio) 環境で
マルチプレーヤーゲームを作るためのツールセットです。

GMnet のマニュアルは http://gmnet.parakoopa.de に置かれていますが、
掲載の元になる形式が https://github.com/Parakoopa/GMnet-manual で公開されています。
それをコピー（GitHub でフォーク）し、翻訳作業を進めているのがこのリポジトリです。


#### 日本語訳方針メモ

* 原文との対応付けの厳密さよりは、滑らかに読んで理解できるようにする事を目指します。
  * 例えば、辞書上の一般的な単語訳よりも文脈において自然な日本語になることを優先し、
    辞書にはない訳出も場合によっては行います。
* しかし、内容を伝える事を優先しすぎて原文から大きく崩れてしまう事は無いようにしたいとも思います。
  * 意味が通じにくいところは、本文中に原文にない言葉を補って独自の作文をしてしまうのを避け、
    訳は若干不恰好なままにして、必要に応じて訳者による注や補足を入れることで対策します。
    * これは読者のためというよりは、さしあたりの翻訳改善作業を容易にするためです。
      独自の作文をしてしまうと単なる文としての翻訳ではなく、
      内容を把握して全体的に見て同じ事を伝えているかを検討する必要があり、
      推敲時に見るべき範囲がむやみに広がってしまいます。これを避けます。
  * 「（訳補：～）」の表記は、自然な日本語に近づけるために、原文には無い言葉を文脈から補っていることを表します。
    そのまま読みつなげられるように言葉を選んでいます。
  * 「（訳注：～）」の表記は、意味がとりにくいと思われる部分に対して追加情報を与えていることを表します。
    一般の書籍で欄外に置いた注意書きと同じ役割です。
    適切な日本語表現が存在しないため原文のニュアンスが訳しきれない場合や、
    原文のままでも内容的に意味が分かりにくいと訳者が感じた場合などにも使います。
  * 「（英：～）」の表記は、直前の単語の辞書的な英語訳を示します。
    説明をしている日本語文とプログラム中の関数名など英語表現との対応が取れるように記します。
  * 「（日：～）」の表記は、直前の単語の辞書的な日本語訳を示します。
    英語のまま表記したほうが良い場合に理解を助けるために記します。
* GameMaker: Studio の専門用語と、例として示されるプログラム上の呼称は
  誤解を避けるためにカタカナなどに置き換えずに英語のまま表記します。
  * ただし一般のコンピュータ専門用語としての意味が取れる文脈では適宜訳します。
* プログラム中のコメントや文字列は訳さず、欄外に訳文を記します。
  * 思わぬミスでプログラムを壊してしまうのを避けるためです。

* さしあたり [チュートリアル](engine/tutorial) 部分を訳してみます。
* 原文原稿と同じくリンクは GitHub サイト上では正しく接続していない場合があります。
  ファイル一覧に戻って適宜選択してください。
* 翻訳作業の都合上、原文をページの後半に残すようにしています。
  * 訳が奇妙だと思われた際に参考に出来るように、という意図もあります。
  * 冒頭に三連のクエスチョンマークがついている部分は、
    訳者が原文に対して疑問に思った事のメモです。
    元リポジトリに対してフィードバックを送ろうかなと考えています。

* 訳者は英語の専門家ではありません。
  プログラミングの知識はありますが GameMaker: Studio については経験が浅いです。
  不適当な部分がありましたら適宜指摘頂けると助かります。


#### 導入簡易ガイド
GMnet を GameMaker: Studio で使えるようにするまでの手順を簡単に述べます。

（訳注：この項は原文にはありません。
どこかに導入マニュアルはあるのかもしれませんが、
訳者が実際にやった操作を参考までにメモしておきます。）

* GameMaker: Studio を起動する。（version 1.4 で確認しました。）
* メニュー Account > Login でログインする。
  （メニュー項目に Manage Account が表示されていたらログイン済みなので先に進む）
* メニュー Marketplace Beta > Marketplace を選択。ウィンドウが開く
* 検索欄（Search the Marketplace と表示されている）に GMnet と入力
* MULTI PLAYER ENGINE と書いてある GMnet の配布パッケージが表示されるのでクリック
* FREE と書いてあるところが購入ボタンなので押す。（無料ですがオンライン購入のステップを踏みます）
* 続く画面で条件などが表示される。下にある Continue ボタンで手続きを続ける。
* 購入完了画面になる。
* このウィンドウの My Library タブを選択する。GMnet ENGINE の項があるので Downloaded ボタンを押す。
* しばらくすると Ready For Use 表示に切り替わる。
* GMnet ENGINE を導入したいプロジェクトを開いておいて、Add to Project を押すと
  取り込み（import）ダイアログが出る。
* 左に自分のプロジェクトが右に GMnet の要素が表示される。
  必要なものを選択して矢印ボタンで取り込み指示を行う。（あるいは Import All で全てを選択）
* OK を押すと取り込まれる。

---

（訳注：以下はこの README の原文です。
マニュアルを執筆する人向けの情報なので訳さずにそのまま残します。）

---
#GMnet Manual pages
This is the repository for the manual pages found on http://gmnet.parakoopa.de.  Each manual page is a markdown page. Just like this readme.


**More information about GMnet products can be found on the website:**  
http://gmnet.parakoopa.de

##Other repositories

* [GMnet ENGINE](https://github.com/Parakoopa/GMnet-ENGINE) (Repository for GMnet ENGINE/CORE/ACCESS and PUNCH)
* [GMnet PUNCH demo project](https://github.com/Parakoopa/GMnet-PUNCH-Demo)
* [GMnet ACCESS demo project](https://github.com/Parakoopa/GMnet-ACCESS-Demo)
* [GMnet GATE.ACCESS](https://github.com/Parakoopa/GMnet-GATE-ACCESS)
* [GMnet GATE.PUNCH](https://github.com/Parakoopa/GMnet-GATE-PUNCH)
* [GMnet GATE](https://github.com/Parakoopa/GMnet-GATE) (Installer and service that combines GATE.ACCESS and GATE.PUNCH)
* [GMnet GATE.TESTER](https://github.com/Parakoopa/GMnet-GATE-TESTER) (Web-based debugging tool for other GMnet GATE producs)

##Structure
The ``/index.md`` file is the index of the manual (http://gmnet.parakoopa.de/manual/)

All subfolders in this repository are **groups** / the individual manuals for the GMnet products (e.g. ``/engine`` for http://gmnet.parakoopa.de/manual/engine).

The files in these directories are the manual pages (e.g. ``engine/versiondifferences.md`` for http://gmnet.parakoopa.de/manual/engine/versiondifferences).

Folders within the groups are subgroups.

The whole structure is also represented in the ``/menu_<group>.xml`` files, which is used as the navigation on the manual pages.

##Links
All links in the manual pages are relative to their group. The link ``[Example](more/example)`` in the manual pages of GMnet ENGINE will redirect to ``<MANUAL INDEX>/engine/more/example``. The markdown page for this page will  be located under ``/engine/more/example.md`` in this repository.

---
