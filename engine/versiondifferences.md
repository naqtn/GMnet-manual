Differences between GMnet ENGINE and GMnet CORE
--------------

**GMnet ENGINE** is the multiplayer engine you can download on this page and on the Game Maker Marketplace. It includes **GMnet PUNCH** to allow multiplayer games between firewalls and an online lobby.

**GMnet CORE** is the core part of ENGINE without PUNCH and can not be downloaded on it's own. To turn GMnet ENGINE into GMnet CORE, simply set ``self.use_udphp`` to ``false`` in ``htme_init()``. You can then even remove all ``udphp_`` scripts then. All manual pages with **PLUS** do not apply to you, if you disabled or removed GMnet PUNCH.

GMnet CORE used to be downloadable as the free version of the HappyTear Multiplayer Engine, the old name of this product.
