---  
layout: post  
title: "SketchUpのWebDialogの使い方"  
published: true  
date: 2012-12-24 08:11  
comments: true  
tags:   
categories:   
---  
  
Trimble SketchUpには、rubyで自動化できる機能があります。  
今日は、rubyで画面を作る、WebDialogというコンポーネントについて  
お話ししたいと思います。  
  
SketchUpには、WebDialogというコンポーネントがあります。    
これを使うとrubyスクリプトから、フォームを作成でき,    
ユーザーと対話的にスクリプトを実行できるわけです。  
  
## WebDialogの特長  
  
- htmlとCSSで、フォームを作成できる  
- rubyスクリプトから、htmlの要素にアクセスできる  
- html内のjavascript関数から、rubyスクリプトを実行できる  
- rubyスクリプトから、html内のjavascript関数を実行できる  
  
## WebDialogは、HTML+CSS+javascript  
  
WebDialogコンポーネントは、フォームのレイアウトをHTMLで指定します。    
また、入力部品の動作はjavascriptで指定します。   
  
基本的な使い方は、公式ヘルプに載っています。    
http://www.sketchup.com/intl/en/developer/docs/ourdoc/webdialog#add_action_callback  
  
## rubyスクリプトの実行方法  
  
あらかじめ、ダイアログに、コールバックメソッドを指定しておく必要があります。  
指定されたコールバックメソッドには、仮想urlが割り当てられており、  
"skp:" + コールバックメソッド名のアドレスに遷移しようとすると、  
コールバックメソッドが実行されます。  
  
仮想urlへ遷移するには、以下のいずれかの方法で指定します。  
  
- リンクのurlとして指定  
- javascript関数内に、window.location="skp:" + 関数名を指定し、ボタンに割り当て  
  
## macの場合はrubyコードが非同期実行  
  
[Martin Rinehart](http://www.martinrinehart.com/models/rubies/ruby2javascript_javascript2ruby.html)によると、  
windows ではjavascriptから呼び出されたrubyスクリプトは同期実行され、  
戻り値をjavasxriptで受け取る事ができるそうです。  
しかし、macではrubyスクリプトは必ず非同期実行のため、  
rubyの戻り値をjavascriptで利用することはできないようです。  
  
注意してください。  
  
## サンプルコード  
  
ほぼ最小構成のWebDialogのサンプルです。  
ここでは、ボタンのクリックイベントにjavascriptのスクリプトを設定し、  
リンクのurlにrubyのコールバックイベントの仮想urlを指定しています。  
  
{% gist 4367009 %}  
      
## サンプルコードの使い方  
  
サンプルコードを実行すると、このような画面が表示されます。  
  
![WebDialogのサンプル](https://www.evernote.com/shard/s75/sh/8f8b089a-0f79-4f18-8faf-fd3e39492230/8371ace36c63afd6fded1e6baa80773b/deep/0/WebDialog001.jpg)  
  
ボタンを押すと、javascriptで作成されたメッセージが表示されます。  
  
![ボタンを押すと、javascriptのアラートが表示される](https://www.evernote.com/shard/s75/sh/801ac46e-8054-4e33-bb96-95187e0cab7c/531face5d8e312d13f234eba2baccd62/deep/0/WebDialog002.jpg)  
  
リンクをクリックすると、rubyで作成されたメッセージが表示されます。  
コード内では、リンクのurlとして、"skp:"に続いてrubyのコールバックメソッド名が  
指定されているのがわかります。  
  
![リンクをクリックすると、rubyのメッセージが表示される](https://www.evernote.com/shard/s75/sh/57a25f6d-39ec-4f93-9780-962e52a0318e/174dbd1151fadda7723fe1b7426c30f5/deep/0/WebDialog003.jpg)  
  
  
## 参考資料  
  
SketchUp Ruby Interface to JavaScript    
<http://www.martinrinehart.com/models/rubies/ruby2javascript_javascript2ruby.html>  
