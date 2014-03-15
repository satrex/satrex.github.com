---  
layout: post  
title: "SketchupのWebDialogで、rubyスクリプトが呼べない時"  
published: false
date: 2012-12-24 12:00  
comments: true  
tags:   
categories:   
---  
  
[前回](http://blog.satrex.jp/blog/2012/12/24/webdialog/)の続きです。  
SketchUpには、WebDialogというコンポーネントがあります。    
これを使うとrubyスクリプトから、フォームを作成でき,    
ユーザーと対話的にスクリプトを実行できるわけです。  
  
## すごくハマったところ  
  
今回、WebDialog経由でrubyスクリプトを実行する際に、  
すごくハマったポイントをお教えします。  
  
動作環境：  
mac OS X 10.8.2  
SketchUp 8.0.4810  
  
それは・・・入力部品の種類です。  
ボタンなどを押した際にjavascriptのコードが実行されるよう、  
動作を設定しているのですが、  
なんと、入力部品の違いによって、動作の一部が実行されません。  
  
## buttonとinput type="button"  
  
結論から言うと、リンクと、\<input type="button"\>で生成したボタンは、  
問題なく動作します。  
  
しかし、\<button\>エレメントで生成したボタンは、  
window.location=でリダイレクトを行う事ができません。  
  
これができないと、javascriptからrubyコードが呼べないのです。  
rubyスクリプトは、javascriptからはurlとして指定する必要があるからです。
  
## サンプルコード  
  
{% gist 4367294 %}  
  
## サンプルコードの使い方  
  
まずはSketchUp上で、コードを実行します。  

実行すると、こんな画面が表示されます。  
![ボタンが２つ、リンクが１つある画面](https://www.evernote.com/shard/s75/sh/b94c926c-0fac-48ad-81a5-4ef3054c6faa/e474f0b5080f91f74e17c112be5d0925/deep/0/WebDialog04.jpg)  
  
１番上のボタンを押すと、ダイアログボックスが１回表示されます。  
  
![javascriptのメッセージ][js]  
  
２番めのボタンを押すと、ダイアログボックスが２回表示されます。  
  
![javascriptのメッセージ][js]  
![rubyのメッセージ][ruby]  
  
リンクをクリックしても、同様に２回表示されます。  
  
３つとも同じ関数を実行しているのに、buttonエレメントだけは、挙動が違います。  
window.locationを指定することができず、rubyのメソッドを呼べません。  
  
ボタンの動作がうまくいかない方は、  
参考にしてください。  
  
次回は、ruby側からjavascriptの関数を呼び出す処理について書こうと思います。

## VimSketchUpのすすめ

余談ですが、これを読んでいらっしゃる貴方は、どうやってサンプルコードを実行していますか？  
Vim上でショートカットを入力するだけで、サンプルコードが実行できたら楽ですよね。  
ちょっと心が動いた方には、[VimSketchUp](http://blog.satrex.jp/blog/2012/06/04/vimsketchup/)をおすすめします。  
  
## 参考資料  
Trimble SketchUp  
<http://www.sketchup.com/intl/en/developer/docs/ourdoc/webdialog#add_action_callback>  
  
Engineering The World     
<http://engineeringtheworld.wordpress.com/2010/02/16/creating-web-dialogs-in-sketchup-and-making-calls-from-and-to-sketchup/>  
  
[js]: https://www.evernote.com/shard/s75/sh/bf295dcd-202d-4bc4-9a1f-853b257fffd3/2408e4d0fe18c83ae73b5cb7fe30c619/deep/0/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202012-12-24%209.51.36.jpg  
[ruby]: https://www.evernote.com/shard/s75/sh/b6109fb2-28db-433a-a0e0-50c73f913727/76121cc80e493c91ecff350b2752d4e3/deep/0/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202012-12-24%2012.36.05.jpg   
