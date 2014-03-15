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

app/assets/stylesheets/application.css を開きます。
ファイルの末尾に、requireを記述したブロックがあるので、
以下の通り追記します。

` *= require active_scaffold `

これも、コメントアウトした感じの見た目で構いません。

![追加したイメージ](https://www.evernote.com/shard/s75/sh/a31327e5-085a-4b7a-bb07-cee7235106f4/6177a9aa3b2ef11108b1ffee2e6f2446/deep/0/スクリーンショット-2014-03-15-14.03.43.png)

#### 4.生成したいエンティティを記述する

エンティティを、ActiveScaffoldを使って、
モデルとコントローラとビューを一気に生成します。
例えば、以下のように記述します。

`rails g active_scaffold work_kind name:string`

#### 5.routesファイルにひとこと書く

最後に、config/routesファイルに、以下のように書きます。
`resources :work_kinds do as_routes end` 

これで、Railsアプリ上では、このように表示されるはずです。

![画面表示](https://www.evernote.com/shard/s75/sh/0db69a4f-26fc-4aa2-9769-53192d74c4f3/755e53bf58e241a358feaf8d737dc9c1/deep/0/スクリーンショット-2014-03-15-16.17.59.png)

#### 間違えるとどうなるか？

ちなみに、requireの記述を間違えると、  
それぞれ特有の動作をします。

stylesheetの記述をミスると、白い背景に文字だけの、
シンプルな画面になります。

![stylesheetの記述をミスった感じ](https://www.evernote.com/shard/s75/sh/9a5860ae-9940-4e47-94d5-b8b70520399d/6d6d562e7cfcc5027ee5e3c6094380e5/deep/0/スクリーンショット-2014-03-15-16.44.05.png)

javascriptの記述をミスると、リンクをクリックしても動作しなくなります。  
ajaxの非同期処理が帰ってこれなくなるのでしょうか。  
『新しいウィンドウで開く』などすると、別窓では表示されるようです。

これは？と思った時は、記述を見なおしてくださいね。当たり前か。


