---
layout: post
title: "さくらのレンタルサーバーにgitをインストールした"
published: true
date: 2012-06-20 19:29
comments: true
tags: 
categories: 
---

[前回の記事][failed]では、さくらのレンタルサーバーにGitを入れようとして失敗しました。
今回は、その解決法を書きます。

## 解決法
パッケージ管理システム経由では入らないようなので、ソースをコンパイルして直接インストールしてしまう事にしました。

gitのtarballからコンパイルしてインストールします。

    mkdir gitinstall  
    cd gitinstall  
    wget https://github.com/git/git/tarball/v1.7.11-rc3 --no-check-certificate
    tar xjvf git-1.7.3.5.tar.bz2
    .cd git-1.7.3.5
    ./configure -prefix=$HOME/local
    gmake
    vi Makefile
    # prefix = $(HOME)/local  を記述
    gmake install

これで、~/local/binにgitがインストールされます。
Makefileを変更しないと、~/binに入ってしまい、具合が悪いようです。

#### 2012/06/22追記：
*~/binに入ってしまうと、組み込みのコマンドと混ざるので、  
環境が汚くなってしまうからかな・・・と思いました。*

## パスを通す

最後に、パスを通します。

    vi ~/.cshrc

set path=( で始まる行を見つけ、括弧の中に、以下を追加します。

    /$HOME/local/bin

直前の文字と、スペースを挟んで区切るのを忘れないでください。
これで、gitにパスが通り、which gitが成功するはずです。
光へ続く道が開かれました。

### 参考文献
[さくらのレンタルサーバーにGitをインストールする方法][install-git]

[install-git]: http://noumenon-th.net/text-hymn/2011/01/git.php
[failed]: http://blog.satrex.jp/blog/2012/06/20/sakura_start/
