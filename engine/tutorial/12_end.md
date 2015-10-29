##12. まとめ / つぎは

ここまでで知るべきことは全て学びました。

GMnet ENGINE を使ったマルチプレーヤー（訳補：ゲームの仕組み）は
これまでのものと少し異なっているかもしれません。
しかし慣れれば可能性は無限です。

ここまでで作ったデモプロジェクトの機能を拡張してみてください。  
（訳補：[9章](tutorial/9_playerlist)で示した）
プレーヤー一覧とチャット表示での名前をプレーヤーがどの room に居ても正しく表示する、
というチャレンジから始めてみてはどうでしょうか。


しばらくエンジンで遊んでみてください。そうすればやがてマスターできるでしょう！

疑問があったり、不具合を見つけたり、新機能の提案があれば、
[サポート](index/#support)に書かれた手引きにしたがってください。

独自パケットを送るなどの、より高度な技法を学びたいのであれば、
"[エンジンの拡張 / 高度な利用](more/extending)" 節を調べてください。

すばらしいマルチプレーヤーゲームの作成を楽しんでください！
もし完成したら私たちに知らせてください。
あなたが作り上げた物をぜひ見たいと思っています。

---

追伸：もしチャレンジにつまづいたら、ここに解答があります。
（シーザー暗号で暗号化されています。アルファベット一文字上方向にずらされています。）

```
Dsfbuf b ofx pckfdu uibu tupsft uif obnf pg uif qmbzfst, jotufbe pg iunf_pck_qmbzfs. Nblf ju qfstjtufou boe tubzBmjwf, tp ju bmxbzt fyjtut. Jo uif qmbzfsmjtu boe uif dibu, mppq pwfs ju jotufbe. Bmufsobujwfmz zpv dbo bmtp tupsf uif obnf pg uif qmbzfst jo uif dibu pckfdut.
```

（訳注：ページの最後に復号と和訳を掲載します。）

---
##12. Conclusion / What's next

You now learned everything there is to know.

Multiplayer with GMnet ENGINE might be a little bit different that what you are used to, but once you got the hang of it, the possibilites are endless.

Try extending the demo project we just created with some features.  
Why not start with our challenge? Fix the player overlay and the chat to display the name of the players corectly, no matter what room they are in.

Play around with the engine for a bit, and eventually you will master it!

If you have any questions, find bugs or have feature suggestions, follow the instructions in the [Support](index/#support) section.

If you want to learn even more advanced trics, like sending your own custom packets, check out the "[Extending the Engine / Advanced Use](more/extending)" section.

    ??? typo "trics" "tricks"

Have fun creating awesome multiplayer games! And if you do, don't forget to  tell us, we really want to see, what you can come up with.

---

PS: If you are stuck with our challenge here's a solution (encrypted with Caesar algorithm, shifted 1 letter in the alphabet up):

```
Dsfbuf b ofx pckfdu uibu tupsft uif obnf pg uif qmbzfst, jotufbe pg iunf_pck_qmbzfs. Nblf ju qfstjtufou boe tubzBmjwf, tp ju bmxbzt fyjtut. Jo uif qmbzfsmjtu boe uif dibu, mppq pwfs ju jotufbe. Bmufsobujwfmz zpv dbo bmtp tupsf uif obnf pg uif qmbzfst jo uif dibu pckfdut.
```

---

PS の 平文：

Create a new object that stores the name of the players, instead of htme_obj_player. Make it persistent and stayAlive, so it always exists. In the playerlist and the chat, loop over it instead. Alternatively you can also store the name of the players in the chat objects.

htme_obj_player の代わりにプレーヤー名を保持する新たな object を作ります。それを persistent かつ stayAlive にして常に存在するようにします。プレーヤー・リストとチャットでは、代わりにそれに対してループします。あるいは、プレーヤーの名前をチャット object に格納することも出来ます。


---

**» Next topic: [PLUS - Bonus 1 - A lobby](./13_lobby)**

« Previous topic: [Creating a chat system](./11_chat)
