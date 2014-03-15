---
layout: post
title: "active_scaffoldが調子いい"
published: true
date: 2014-03-15 10:33
comments: true
tags: 
categories: 
---

### ActiveScaffoldとは

Railsアプリでは、CRUD操作（登録・修正・表示・削除）を
一気に作ってくれる、Scaffoldという機能があります。
が、あまり実用的ではない、という定評で、
便利な機能にもかかわらず、それほど使われていません。

そこでActiveScaffoldです。
ActiveScaffoldでは、ごく少ない操作で、
かなりそれっぽい画面を自動生成してしまいます。

### 使い方

1. gemで導入
2. javascriptテンプレートにrequireを書く
3. stylesheetテンプレートにrequireを書く
4. 生成したいエンティティを記述する
4. routesファイルにひとこと書く

#### 1.gemで導入

Gemfileに、以下の通り記述します。
`
gem install active_scaffold
`

関係ないですが、僕は最近、もっぱらskip_bundleオプション付きでプロジェクトを作り、  
後からプロジェクト内のvendor/bundle配下にgemをインストールするのが、  
全体の環境を壊さなくていいなぁとお気に入りです。

#### 2. javascriptテンプレートにrequireを書く

![ファイルイメージ](https://www.evernote.com/shard/s75/sh/1de3951c-0238-4ec6-95a0-06065d091c4b/fc3a7db781b87e66da4db12924eea67a/deep/0/スクリーンショット-2014-03-15-13.31.28.png)

app/assets/javascripts/application.js を開きます。
ファイルの末尾に、requireを記述したブロックがあるので、
以下の通り追記します。

` //= require active_scaffold  `

コメントアウトした感じの見た目で構いません。
![追加したイメージ](https://www.evernote.com/shard/s75/sh/76734574-ca91-4172-a070-0b1ee230f80f/83ae886c65eec413d1ad1cf73e124516/deep/0/スクリーンショット-2014-03-15-14.03.06.png)

#### 3. stylesheetテンプレートにrequireを書く

![stylesheetテンプレートはこれ](https://www.evernote.com/shard/s75/sh/46af7df5-867a-488d-b83e-77f8b458d6c9/be9a33261184f6fb0dfb4c305ecf01bc/deep/0/スクリーンショット-2014-03-15-14.03.27.png)

