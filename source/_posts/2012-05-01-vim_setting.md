---
layout: post
title: "vimの設定見直し中"
published: true
date: 2012-05-01 22:43
comments: true
tags: vim
categories: 
---

vimの設定を見直しています。
最近zshを使うようになって、gvimのコマンドラインに不便を感じるので、
コマンドラインから起動するモードでも便利にやれたらいいなぁと思っています。

今の設定で行くと、いろいろと超えないといけない壁がある感じです。

### NeoComplCacheが使えない
最大の問題は、NeoComplCacheがコマンドラインからは使えないこと。  
rbファイルやHTMLファイルを編集しようとすると、
ファイルを開いた時か保存した時のどちらかに、猛烈な勢いでエラーを吐きまくります（詳細は画像参照）。

もう一点重大な問題として、日本語入力などの設定が、コマンドラインからのVimでは不便すぎます。

- IMEが全ての入力に優先している。  
Vimのモード切替などは、日本語入力中でも、半角で受け付けてくれないと不便です。
- Insertモードにすると、カーソルキーでカーソルが移動できない（A〜Dの入力で代替される）。
  set nocompatibleと, imap ^[OA <Up>を試した結果、改善されないので諦めました。 

基本はGvimを立ち上げるが吉、で当面やってみようかと思います。
むしろGvimのコマンドラインがzshになってくれたら文句ないんですが、
Vimのコマンドでlessを使うたびに、『ターミナルの全機能が使えるなんて思うなよ』と言われてしまうので、
半ば諦めています。おわり。

### エラーメッセージの画像

<div class="thumbnail"><a href="https://skitch.com/sat-rex/8aqq2/tmux-114x44"><img style="max-width:638px" src="https://img.skitch.com/20120502-ep9y7r2mj68ey3rcgdmy2u86kj.medium.jpg" alt="tmux-114×44" /></a></div>
<div class="thumbnail"><a href="https://skitch.com/sat-rex/8axfu/tmux-114x44-1-3"><img style="max-width:638px" src="https://img.skitch.com/20120502-cb8ih2ksrnnfxk7bkgsujpk1ud.medium.jpg" alt="tmux-114×44-1-3" /></a></div>
<div class="thumbnail"><a href="https://skitch.com/sat-rex/8axrb/tmux-114x44-3"><img style="max-width:638px" src="https://img.skitch.com/20120502-tt6iku576gwk3sx96yeh32jspx.medium.jpg" alt="tmux-114×44-3" /></a></div>
