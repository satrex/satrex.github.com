---
layout: post
title: "VimSketchUpをリリースしました"
published: true
date: 2012-06-04 00:38
comments: true
tags: 
categories: 
---

VimでSketchUpのRubyスクリプトを書きたい方に朗報です。
VimでSketchUpRubyを実行できるプラグインをリリースしました。

## 動作のイメージ

例えば、スクリプトで三角形を描いてみます。
初めに、SketchUpを起動します。
これが初期画面。ちなみに、女の子の名前はサンちゃんです。

![SketchUpの初期画面][before]

何もないところに、Rubyスクリプトで三角形を描きます。
まず、VimでSketchUp用のスクリプトを書きます。

![VimでRubyスクリプトを書いたところ][inputting]

そして、”￥sur”とキーボードで入力すると、
SketchUpの画面に変化が起きます。

![三角形が出たところ][after]

三角形が描けました。

## GitHubに登録しました

このスクリプトを、GitHubに登録しました。
リポジトリは[ここです][git-repo]。

## これから

インストールの仕方、初期設定など、
使い方に関する記事を書きます。

VimでSketchUpRubyが書けるようになったからには、
補完の支援を受けたり、SketchUpAPIのヘルプをローカルで
見たりできるようになりたいです。

Rubyの補完は弱いので限界はあるのですが、
現在はdictファイルを使って、補完に挑戦しています。

## 感想

前々から作りたいと言っていたプラグインです。
やっと完成を見ることができました。
長かったです。

相変わらず、VimScriptもSketchUpAPIも手探りですが、
困るのに慣れてきました。

[before]: https://img.skitch.com/20120603-bi3hcwd594ubauj132rkhkwk92.gif
[inputting]: https://img.skitch.com/20120603-e29j4n2sq9hk15mmfrqj461sib.gif
[after]:https://img.skitch.com/20120603-jmbeicj5qw2xp1rmujb42cqub.gif 
[git-repo]: https://github.com/satrex/VimSketchUpRuby
