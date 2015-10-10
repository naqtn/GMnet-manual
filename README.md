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
### About this fork ( https://github.com/naqtn/GMnet-manual )

This repository is for my Japanese translation trial.

#### 方針メモ

* 原文との対応付けの厳密さよりは、滑らかに読んで理解できるようにする事を目指します。
* しかしあまり原文から崩す事の無いようにしたいと思います。
  * 意味が通じにくいところは、本文中に原文にない言葉を補って独自の作文をしてしまうのを避け、
    訳は若干不恰好なままにして、必要に応じて訳者による注や補足を入れることで対策します。
* Game Maker: Studio の専門用語は誤解を避けるためにカタカナに置き換えずに英語のまま表記します。
  * ただし一般のコンピュータ専門用語としての意味が取れる文脈では適宜訳します。
* 訳者は英語の専門家ではありません。
  プログラミングの知識はありますが Game Maker Studio については経験が浅いです。
  不適当な部分がありましたら適宜指摘頂けると助かります。

* さしあたり [チュートリアル](engine/tutorial) 部分を訳してみます。
* 原文原稿と同じくリンクは GitHub サイト上では正しく接続していない場合があります。
  ファイル一覧に戻って適宜選択してください。
