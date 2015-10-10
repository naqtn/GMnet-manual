GMnet ENGINE と GMnet CORE の違い
--------------

**GMnet ENGINE** はこのページと Game Maker Marketplace でダウンロードできるマルチプレーヤー・エンジンです。
これは、ファイヤーウォール間でのゲームとオンライン・ロビーを提供する **GMnet PUNCH** を含みます。

**GMnet CORE** は PUNCH を除く ENGINE のコア部分で、それだけをダウンロードする事はで来ません。
GMnet ENGINE を GMnet CORE にするには、
``htme_init()`` の中の ``self.use_udphp`` を ``false`` にします。
スクリプト中の ``udphp_`` は削除できます。
GMnet PUNCH を無効にする（もしくは取り除く）と、
マニュアルページの  **PLUS** がついているページは適用されなくなります。

GMnet CORE （訳補：という名称）は、
HappyTear Multiplayer Engine（これはこのプロダクトの古い名前）のフリー版として使われてきました。


----
Differences between GMnet ENGINE and GMnet CORE
--------------

**GMnet ENGINE** is the multiplayer engine you can download on this page and on the Game Maker Marketplace. It includes **GMnet PUNCH** to allow multiplayer games between firewalls and an online lobby.

**GMnet CORE** is the core part of ENGINE without PUNCH and can not be downloaded on it's own. To turn GMnet ENGINE into GMnet CORE, simply set ``self.use_udphp`` to ``false`` in ``htme_init()``. You can then even remove all ``udphp_`` scripts then. All manual pages with **PLUS** do not apply to you, if you disabled or removed GMnet PUNCH.

    ??? You can then ... then
    ??? Excess twice "then" ?

GMnet CORE used to be downloadable as the free version of the HappyTear Multiplayer Engine, the old name of this product.
