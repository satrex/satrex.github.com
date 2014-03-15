---
layout: post
title: "Octopressのインストール（後編）"
published: true
date: 2012-04-23 23:05
comments: true
tags: octopress
categories: 
---

[前編][part1]の続きです。

## Octopressのインストール
いよいよOctopressをインストールしていきます。
公式サイトやGlideNoteさんの記事、またjedipunkzさんの記事が参考になります。

- [GithubとOctopressでモダンな技術系ブログを作ってみる - GlideNote][GlideNote]
- [github.com で Octopress 構築 - jedipunkz][jedipunkz]

![Octocatに似たデザインのmac](https://www.evernote.com/shard/s75/sh/1c5fcc0f-7c94-45ba-9f7d-c9c6909bdfb6/a28bb5b09a4b9d7cc11c78e691395ddd/res/0e3d3046-3527-4e16-bc47-53ff68a3a9df/mac_ball-20120423-205850.jpg.jpg)

## GithubPageの取得
[Githubの新規プロジェクト画面](https://github.com/new)から、好きな名前でブログ用のリポジトリを作っておきます。

![Githubから、ブログ用のリポジトリを作る](https://img.skitch.com/20120424-nt9u7frxprtchkn31au43ewe4w.jpg)

## Octopressのインストールのイメージ
Octopressのインストールがどんな感じかというと、  
AppStoreでアプリを買うのとは、だいぶ趣きが違います。  

すごく基本的なところから解説してみます。
Octopressは、『アプリケーション』フォルダに入るプログラムではありません。
ひとつのフォルダを作ってそこにインストールし、そのフォルダをブログの基地として使うイメージです。

![1フォルダに、ツールと記事が同居します](http://farm8.staticflickr.com/7274/7109487325_fc55531d8a.jpg )
## Octopressのインストール

    mkdir ユーザー名.github.com  
    cd  ユーザー名.github.com  
    git clone git://github.com/imathis/octopress.git octopress  
    cd octopress  
    gem install bundler  
    bundle install  
    rake install # classic テーマのインストール


こんな感じで入れて下さい。
上の例だと、~/ユーザー名.github.com/octopress 
のようになります。

別にアカウントごとにフォルダに分ける必要がなければ、
~/octopress/ のように構成しても問題ないです。
その場合は、上のコマンドの最初２つを飛ばします。

## Octopressの構成

インストールしたOctopressのフォルダ構成と、動作のイメージを紹介します。

![_config.yamlは設定ファイル、sourceに記事やスタイルを記述、publicにhtmlとCSSが生成される](https://www.evernote.com/shard/s75/sh/7d825d5b-1923-40c5-8d00-4237ff243e17/6bffbb3957614d2fa4438e7e0ccfa423/res/21ae89ae-4b24-4cf5-a03d-2fbc58a53742/octopress-20120423-154359.jpg.jpg)

上の図で示すとおり、Octopressのフォルダ構成は、Octopressフォルダの中にいろいろある感じです。  
コマンドラインで作業する時には、基本的にカレントディレクトリは『Octopress』フォルダです。  

参考資料；
 [ Octopressをインストールする動画 ： burnsoft ][Octopress_movie]  
英語ですが、作業の流れがわかりやすいです。

## Octopressの初期設定
Octopressの初期設定を行います。

    rake setup_github_pages
    Enter the read/write url for your repository:

上で作成したGithub PagesのリポジトリURLを指定します。
オイラの場合だとこうです。

    git@github.com:satrex/satrex.github.com.git

    rake generate
    rake deploy


しばらくすると http://satrex.github.com/ にアクセス出来るようになります。

### _config.ymlの設定
octopressフォルダにある、_config.ymlを変更し、ブログの設定を行います。

    url:                # For rewriting urls for RSS, etc
    title:              # Used in the header and title tags
    subtitle:           # A description used in the header
    author:             # Your name, for RSS, Copyright, Metadata
    simple_search:      # Search engine for simple site search
    subscribe_rss:      # Url for your blog's feed, defauts to /atom.xml
    subscribe_email:    # Url to subscribe by email (service required)
    email:              # Email address for the RSS feed if you want it.


設定終了後は、`rake gen_deploy`でデプロイできます。


## 記事の投稿

ターミナルで、次のコマンドを実行します。

    rake new_post["title"]
    rake new_post\["title"\] # zsh の場合

octopress/source/-postsフォルダに、『日付-title.markdown』のようなファイルが生成されます。
それを、好きなエディタで編集します。

Markdownという記法を使います。
オイラはVimでやっていますが、まったく予備知識がない場合は、[Byword](http://www.bywordapp.com)というエディタをおすすめします。
Markdownのプレビュー機能が付いているので、書いた記事がどう見えるのか確認しやすいはずです。

## トラブルシューティング

作業をしてて困った事を、ここにメモとして残しておきます。

### rake installで、バージョンエラーが出る

お使いのPCに入っているrakeが新しすぎると起こるようです。
[RVMの設定やインストールを見直し][rvm_install]、バージョンを合わせます。
`bundle exec rake install`と表記すると回避できます。

### rake generateで、コンパイルエラーが出る
posix-spawnなどのエラーに悩みました。
GCCの問題で起こるようです。
[GCCのインストール][gcc_install]の項を見直してください。

### 参考資料

- [GithubとOctopressでモダンな技術系ブログを作ってみる - GlideNote][GlideNote]  
  Octopressインストール記事の草分けではないかと思います。
- [github.com で Octopress 構築 - jedipunkz][jedipunkz]  
  Linuxを使ったインストールについてまとまっています。
- [Octopressでブログ構築 - あるふぁ世界線][alpha]  
  どうしてOctopressを使うか、とかも書いてあって、参考になります。一読をお薦めします。


[alpha]: http://www.homux2.net/blog/blog/2012/03/30/blog-build/
[part1]: http://satrex.github.com/blog/2012/04/23/installed-octopress-001/
[gcc_install]: http://satrex.github.com/blog/2012/04/23/installed-octopress-001/#gcc_install
[rvm_install]: http://satrex.github.com/blog/2012Octopress_movie/04/23/installed-octopress-001/#rvm_install
[GlideNote]: http://blog.glidenote.com/blog/2011/11/07/install-octopress-on-github/
[jedipunkz]: http://jedipunkz.github.com/blog/2012/03/20/github-dot-com-de-octopress-gou-zhu/
[Octopress_movie]: http://burnsoft.github.com/blog/blog/2011/09/23/octopress-install-with-screencast/



