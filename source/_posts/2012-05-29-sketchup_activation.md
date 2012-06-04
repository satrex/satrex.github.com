---
layout: post
title: "MacでSketchUpのRubyスクリプトを自動実行"
published: true
date: 2012-05-29 21:39
comments: true
tags: 
categories: 
---

以前に書いていた、GoogleSketchUpのコードをVimから書けるプラグインを書いています。

Windowsでは、Bridgeという神アプリで、Eclipse上から
SketchUpを操作する事ができますが、macには対応しません。

## AppleScriptでなんとかしてみた

そこで、macで実行中のSketchUpでRubyコードを実行できる
AppleScriptを書きました。

これをVimから実行することで、Vimで書いているRubyスクリプトを、
SketchUp上で実行する事ができるはずです。

Bridgeと比べると格段にしょぼい作りですが、
今までの面倒に比べれば天と地の差です。

## 現状
とりあえず、SketchUpが最前面に出て、Rubyコンソールが開き、
クリップボードの文字列をペーストするだけです。

Vim側はまだありません。

## 次のアクション

Vim側で、バッファの全文字列を取得する処理＋
このAppleScriptを呼び出す処理を書けば、
うまくいくかも知れません。

SketchUpスクリプトファイルのフォルダは込み入ったパスにあるので、
新規作成機能も欲しいです。

glidenoteさんのOctoEditorをForkして作ってみようかな・・・
と考えています。

## ソース

<script src="https://gist.github.com/2829474.js"> </script>


