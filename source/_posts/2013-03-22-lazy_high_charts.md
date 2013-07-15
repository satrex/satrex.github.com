---
layout: post
title: "lazy_high_chartsを使ってみた"
published: true
date: 2013-03-22 07:28
comments: true
tags: 
categories: 
---

### Lazy high chartsを使ってみた

railsでグラフを表示させたくて、
Lazy high chartsを使ってみました。
やった事を書いておきます。

### なんでLazy high chartsなの？

Lazy high chartsを選んだ理由は、以下の通りです。

1. 『Web グラフ』で検索したら、high chartsの評判がよかった  
    →[webアプリ(perlやjavascript)でグラフ表示なら、Highcharts で決まりかも](http://d.hatena.ne.jp/end0tknr/20111218/1324206587)
2. 『ruby high charts』で検索したら、Lazy high chartsの記事を見つけた  
    →[Rails で Lazy high charts を使ってチャートを実装してみた](http://tnakamura.hatenablog.com/entry/20120528/rails_lazy_high_chart)

というわけで、Lazy high chartsを使ってみます。

### まずはインストール

[上記のサイト](http://tnakamura.hatenablog.com/entry/20120528/rails_lazy_high_chart)を参考に、Lazy high chartsのインストールを行います。

まず、Gemfile に
`` gem 'lazy_high_charts' ``

を追加しました。
そして、
`` bundle `` を実行します。インストールが始まりました。  
ここまでは問題ありません。

そして、

bundle exec rails g lazy_high_charts:install

を実行すると、highchart.js がダウンロードされて、assets/javascripts に配置される・・・  
はずでしたが、何やらエラーが表示されました。

### インストールエラー 

エラーメッセージは、次のようなものでした。

`` 
% /projects/rails/lazy_chart% bundle exec rails g lazy_high_charts:install
[WARNING] Could not load generator "generators/lazy_high_charts/install/install_generator". Error: uninitialized constant LazyHighCharts::Rails::Generators.
/.rvm/gems/ruby-1.9.3-p0/gems/lazy_high_charts-1.4.0/lib/generators/lazy_high_charts/install/install_generator.rb:4:in `<module:LazyHighCharts>'
/.rvm/gems/ruby-1.9.3-p0/gems/lazy_high_charts-1.4.0/lib/generators/lazy_high_charts/install/install_generator.rb:3:in `<top (required)>'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:300:in `block (2 levels) in lookup'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:296:in `each'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:296:in `block in lookup'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:295:in `each'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:295:in `lookup'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:152:in `find_by_namespace'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:169:in `invoke'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/commands/generate.rb:12:in `<top (required)>'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/commands.rb:29:in `<top (required)>'
script/rails:6:in `require'
script/rails:6:in `<main>'
Could not find generator lazy_high_charts:install.
`` 

このエラーについて調べたところ、次の記事が見つかりました。

[Problem with rails g lazy_high_charts:install](https://github.com/michelson/lazy_high_charts/issues/91)  
どうやら、Railsのバージョンが3.1以上の場合は、  
app/assets/javascripts/application.jsに次の行を追加しないといけないようです。

<code>
//= require highcharts   
//= require exporting
</code>

これで、エラーは解決したでしょうか。

`` 
% /projects/rails/lazy_chart% bundle exec rails g lazy_high_charts:install
[WARNING] Could not load generator "generators/lazy_high_charts/install/install_generator". Error: uninitialized constant LazyHighCharts::Rails::Generators.
/.rvm/gems/ruby-1.9.3-p0/gems/lazy_high_charts-1.4.0/lib/generators/lazy_high_charts/install/install_generator.rb:4:in `<module:LazyHighCharts>'
/.rvm/gems/ruby-1.9.3-p0/gems/lazy_high_charts-1.4.0/lib/generators/lazy_high_charts/install/install_generator.rb:3:in `<top (required)>'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:300:in `block (2 levels) in lookup'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:296:in `each'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:296:in `block in lookup'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:295:in `each'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:295:in `lookup'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:152:in `find_by_namespace'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/generators.rb:169:in `invoke'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/commands/generate.rb:12:in `<top (required)>'
/.rvm/gems/ruby-1.9.3-p0/gems/railties-3.2.13/lib/rails/commands.rb:29:in `<top (required)>'
script/rails:6:in `require'
script/rails:6:in `<main>'
Could not find generator lazy_high_charts:install.
``

じゃん。
やっぱり出ますね。

しかし、[くだんの記事](https://github.com/michelson/lazy_high_charts/issues/91)によると、どうやらこれでも問題なく動作するらしいです。
  

### では、動かしてみますか

それでは、警告を気にせず、動作させてみます。

`` rails s ``

![棒グラフ](https://www.evernote.com/shard/s75/sh/dbf05acf-97e1-4240-bf3b-90ec9d767ce1/57f93850b06d68a14848495f769e4bc6/deep/0/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202013-03-23%2022.52.57.jpg)

グラフが出ました。

あとは、データの取得がうまくできれば、楽しく暮らせそうです。

