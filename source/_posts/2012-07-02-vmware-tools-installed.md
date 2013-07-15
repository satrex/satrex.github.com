---
layout: post
title: "ゲストubuntuに、VMware-Toolsをインストールする"
published: true
date: 2012-07-02 19:42
comments: true
tags: ssh wordpress
categories: 
---

ゲストOSの仮想サーバーへ、ホストOSからssh接続するために、  
公開鍵を渡します。  
今回は、ホストの共有フォルダ経由でファイルを渡します。  

ホストOSの共有フォルダを使うには、VMware-Toolsが必要です。  
VMwareToolsをインストールする方法を解説します。  

## VMWare Toolsの導入

1. VMware-Toolsの仮想CDを挿入
2. カーネルの番号を確認する
3. カーネルヘッダーをインストールする
4. VMware-Toolsをインストールする
 
### VMwareToolsの仮想CDを挿入

VMwareFusionのメニューから、『仮想マシン->VMWareToolsのインストール』を選択します。  
その後、以下のように仮想CDをマウントします。

    $ sudo mkdir -p /mnt/cdrom
    $ sudo mount /dev/cdrom /mnt/cdrom
    > mount: block device /dev/sr0 is write-protected, mounting read-only

ここでインストールを行うと、失敗します。

    tar xzvf /mnt/cdrom/VMwareTools-8.8.4-730257.tar.gz 
    cd ./vmware-tools-distrib/
    sudo ./vmware-install.pl 
    
    ...
    
    Searching for a valid kernel header path...
    The path "" is not valid.
    Would you like to change it? [yes] 

カーネルヘッダーがないとだめだそうです。  

### カーネルのバージョンを確認する

メニューから、『仮想マシン->設定->ネットワークアダプタ』を選択し、  
ネットワークにブリッジ接続を指定します。

カーネルのバージョンを確認し、適切なヘッダーを取得します。
     
    uname -a

    `linux 3.2.0-24-virtual #39-ubuntu SMP Mon May 21 18:44:18 UTC 2012 x86_64 x86_64 x86_64 GNU/Linux`  
このカーネルバージョンは、3.2.0-24-virtual だということがわかりました。

### ヘッダーファイルをインストールする

ヘッダーファイルをインストールします。

    sudo apt-get install linux-headers-3.2.0-24-virtual

バージョンのないヘッダーファイル（linux-headers-virtual）も存在しますが、  
自分の環境では、サーバー接続エラー（404）が発生して、  
インストールが成功しませんでした。 

### VMware-Toolsをインストールする

もう一度、VMware-Toolsをインストールします。

    sudo ./vmware-install.pl -d
    
    Searching for a valid kernel header path...
    Detected the kernel headers at "/lib/modules/3.2.0-24-virtual/build/include".
    The path "/lib/modules/3.2.0-24-virtual/build/include" appears 
    to be a valid path to the 3.2.0-virtual kernel headers.
    Would you like to change it? [no]

今度は、カーネルヘッダーを認識しているようです。
正しくVMware-Toolsがインストールされました。

## おわりに

これをちゃんと読む人はとても少ないはずですが、
いるとすれば、とても困っている方でしょう。

この記事が少しでもお役に立てれば嬉しいものですね。


ちなみに・・・本当は、ゲストOSにsmbclientを入れれば  
ホストOSの共有フォルダにアクセスできると思うのですが、  
設定がうまくいかず、今回はあきらめました。

## 参考資料 

CentOS 5.5 x86 に VMware Tools をインストールする  
<http://d.hatena.ne.jp/yohei-a/20101222/1293051179>


