---
layout: post
title: "Three.jsを試してみた"
published: true
date: 2012-05-22 19:50
comments: true
tags: 3D, JavaScript
categories: 
---

[krayさんのサイト][sampleArticle]を丸写しで、Three.jsを試してみました。
うまくいったので、お礼かたがた書いてみます。

### うまくいったこと

いくつか、これは助かったなぁと思う事を書いてみます。
#### Three.jsの扱い

まず[ソース][threeJsSource]をCloneして、さてどう使うんだろうと考えちゃいました。
そうだ[ReadMe][threeJsReadme]を見よう、という事で見てみると、minimize版をHTMLヘッダーで参照すればいいとのこと。

![３Dの立方体がぐりぐり動く][sampleImage]

なるほど。
チュートリアルやwikiも充実してるようなので、しばらく入り浸ってみたいです。

### FireFoxのいいところ

とくに他のブラウザと比較しての話ではないです。
cmd-uでソースの表示。そこからリンクを辿ってスクリプトなど見れるので、追いかけやすいなぁと。
強いて言えば、ソースにシンタックスハイライトしてくれれば最高です。

あと、３DでDOMツリーが見れるのが面白いです。

## うまくいかなかったこと

逆に、これはまだよくわかってないぞ、という部分について。

### javascriptの補完

neocomplcacheがないVimは使いません。というくらい、オイラは補完が好きです。
補完がないとコードが書きたくないです。
で、javascriptのシンタックスや、Three.js内のメソッド名など、持ってきてほしいものがいくつかありました。

あとでneocomplcacheのヘルプをよく読んでみます。

### SketchUpとThree.jsの連携

SketchUpでモデリングして、Webサイトに載せてぐりぐり動かす、とかできると最高です。

SketchUpはWindows版だとBridgeというライブラリでEclipseからスクリプトが実行できるのですが、いかんせんmacではBridgeが通用せず。
まだレベルが足りなくて、Bridgeを移植しようにも、どう手をつけていいのかわかりません。

VimからSketchUpのRubyコンソールのウィンドウハンドルを取って、文字を入力してExecuteScriptコマンドを流せばいいはずです。

でもどうすればそれができるか分かりません。
ざんねん。
いつかは！ 

(2012/12/24 追記)
できました。
次の記事を参照してください。

http://blog.satrex.jp/blog/2012/06/04/vimsketchup/

[sampleArticle]: http://kray.jp/blog/three-js/
[threeJsSource]: https://github.com/mrdoob/three.js/
[threeJsReadme]: https://github.com/mrdoob/three.js/#readme





