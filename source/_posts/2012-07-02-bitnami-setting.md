---
layout: post
title: "bitnamiの仮想マシンを使うためのステップ"
published: true
date: 2012-07-04 07:35
comments: true
tags: ssh wordpress
categories: 
---

WordPressを使ったWebサイト作りをしようとしています。
ローカルの仮想サーバーでサイトのソースをGitに上げ、
公開用のサーバーでGitからPullすることで、デプロイする構成です。

そこで、ローカルの仮想サーバーには、
WordPressとMySQLとPHPのスタックである、
bitnamiを使ってみます。

## bitnami仮想マシンのダウンロード

bitnamiを使うためには、２つの方法があります。

1. 既存の仮想マシンに、bitnamiをインストールする
2. bitnamiインストール済の仮想マシンを、新規にダウンロードする

今回は、2.を解説します。
公式サイトから、bitnamiがインストールされた仮想マシンをダウンロードします。

## sshの導入

コマンドラインから操作するため、仮想マシンでsshを有効にします。
公開鍵の受け渡しが、最も苦労した部分です。

### 公開鍵の渡し方

仮想サーバーの公開鍵を、開発用マシンに渡すための方法は、
次のような選択肢があります。

1. 仮想マシンがSmabaサーバーとなり、ホストOSのがクライアントとなってファイルを受け渡す
2. 逆に、ホストOSの共有フォルダに、仮想マシンからアクセスしてファイルを受け渡す
3. GitHubなど、外部ストレージを経由してファイルを受け渡す

ここでは、2.を解説します。

### VMware-Toolsの導入

ホストOSの共有フォルダにゲストOSからアクセスするには、  
VMware-Toolsをインストールします。

別の記事にまとめていますので、参照してください。
[vmware-tools-install]

### ssh鍵の生成

ホストOSで、以下のコマンドを入力します。

    sudo ssh-keygen

画面に従ってパスワードを入力すると、公開鍵と秘密鍵が生成されます。
id_rsa.pubファイルが公開鍵、id_rsaファイルが秘密鍵です。

### 公開鍵を、共有フォルダに置く

これから、いまホストOSで作った公開鍵をサーバーに渡します。    

まず、id_rsa.pubファイルを、ホストOSの共有フォルダにコピーします。
オイラの環境では、Macの~/shareフォルダです。

マウスでポイっと入れればOKです。

### ゲストubuntuに、ホストOSの公開鍵をインストール

共有フォルダに入れた公開鍵を、ゲストOSから見てみます。

    $ ls /mnt/hgfs/share
    > id_rsa.pub

ホストOSの公開鍵が見えています。
これを、ゲストOSにインストールします。

でも、いったいどこにインストールするのでしょうか？

サーバーには『この鍵をくれたマシンのアクセスには応じるよ』というファイルがあります。  
authorized-keysというファイルです。
今回受け取った公開鍵を、authorized_keysファイルに追記します。

このファイルには、複数の鍵を書き込むことができます。
上書きすると、今までアクセスできたマシンがアクセスできなくなる、
という現象が起こりますよ。

    cat /mnt/hgfs/share/id_rsa.pub >> /home/bitnami/.ssh/authorized_keys

**\>\>に注目。**

これで、ゲストOSに、ホストOSの公開鍵がコピーされました。

## sshの設定

ゲストOSで、以下のコマンドを実行します。

    $ sudo vi /etc/ssh/sshd_config

以下の行を探して、下のように変更します。

  ChallengeResponseAuthentication no
  PasswordAuthentication no
  UsePAM no

## sshデーモン、いでよ！

ゲストOSがアクセスを待ち構えるために、
sshデーモンを召喚します。
このデーモンが、サーバーの門番を務めてくれるわけです。

召喚の呪文は、これです。

    $ sudo start ssh

これで、ゲストOS上でsshが有効になりました。

## ホストOSからアクセスしてみる

ホストOS上で、sshコマンドを入力します。

    ssh 192.168.100.xxx（ゲストOSのIPアドレス）-l bitnami

ゲストOSのIPアドレスは、ゲストOSでifconfigコマンドを使用すると、  
表示されます。  
・・・大丈夫ですよね？？

あと、-l bitnamiの部分がなんなのかというと、
bitnamiユーザーでログインします、という意味です。
サーバーにはbitnamiユーザーしかいないため、
他のユーザーではログインできません。

別のユーザーを作っている場合は、
そのユーザー名を指定してください。

これを指定しない場合は、ホストOSのユーザー名でログインします。

    $ ssh 192.168.100.101 -l bitnami         
    > The authenticity of host '192.168.100.101 (192.168.100.101)' can't be established.
    > RSA key fingerprint is 86:74:fe:6b:8b:b1:c2:64:3f:d0:80:bc:92:f3:c0:75.
    > Are you sure you want to continue connecting (yes/no)? yes

何か聞かれた場合は、yesと答えて下さい。

    > Warning: Permanently added '192.168.100.101' (RSA) to the list of known hosts.
    > Last login: Tue Jul  3 13:10:37 2012

これで、sshログインできました。  
めでたし。


[faq]: http://bitnami.org/faq/virtual_machines
[vmware-tools-install]: /2012-07-02-vmware-tools-installed.html

