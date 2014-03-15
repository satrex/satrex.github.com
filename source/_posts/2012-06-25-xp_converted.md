---
layout: post
title: "ConverterでXPマシンを仮想化するために必要な4つのこと"
published: true
date: 2012-06-25 22:47
comments: true
tags: 
categories: 
---

これをお読みの皆さんは、仮想マシンを使っておいででしょうか？  
Windows XPのマシンを、macのVMWareで使うために仮想化しました。  
そこでハマったポイントを、後に続く方のためにまとめておきます。

## 環境

ホストOS：mac OSX (Lion) 10.7.4  
実行環境：VMWare Fusion 4.1.3  
仮想化するマシンのOS：Windows XP Pro  
仮想化するアプリ： VMWWare Converter 5.0.0

## ポイント

1. VMWare Converterをダウンロードして使う
　（VMWare Fusion付属のMigrationAgentは使わない）
2. WindowsXPのCD-ROMから、sysprepファイルをコピーする
3. 仮想化するマシンは、十分に容量を減らしておく
4. 仮想化するマシンのVolume Shadow Copyサービスを有効にする

### 1.VMWare Converterをダウンロードして使う

明らかに、速さも信頼性も、Converterのほうが上です。  
物理マシンを吸い出す目的のためには、ぜひConverterを使うべきです。  

以下のURLからダウンロードして、XPマシンにインストールしてください。  
構成について尋ねられます。  
『ローカル』と『クライアントサーバー』の二択から、『ローカル』を選びます。  

### 2.WindowsXPのCD-ROMから、sysprepファイルをコピーする

公式ヘルプなどでsysprepと呼ばれるものは、以下の圧縮フォルダのファイル一式です。  
(OSのディスク)￥￥SUPPORT￥TOOLS￥  

![sysprepツール](https://img.skitch.com/20120625-b7a5a973xx41ic6qje142y627i.gif)

これを、以下のパスに保存します。

    C:\Documents and Settings\All Users\Application Data\VMware\VMware vCenter Converter Standalone\sysprep\xp

保存するパスは、VMWareConverterを実行すると教えてくれます。  
全ファイルまとめて保存して構いません。

### 3.仮想化するマシンは、十分に容量を減らしておく

具体的には、次のような事をします。

- ディスクのクリーンアップ
- アプリケーションの削除
- データを外部に移動

これが足りていないと、次のエラーが発生するようです。

    Failed to create VSS snapshot of source volume. Error code: 2147754783(0x8004231F). 

### 4.仮想化するマシンのVolume Shadow Copyサービスを有効にする

コントロールパネルから、『管理ツール->サービス』を選択し、  
サービス一覧を表示します。
一覧からVolume Shadow Copy Serviceを捜し、  
『スタートアップの種類』を『自動』に設定します。

![コンパネ→管理ツール] (https://img.skitch.com/20120625-ghgec3kruxiirgkmkd6k1wftjm.gif)
![サービス] (https://img.skitch.com/20120625-q1f2a5d35a8bjj7kqhpbixbxj5.gif)

これが足りていないと、次のエラーが発生します。

    FAILED: Unable to create a VSS snapshot of the source volume(s). Error code: 2147754758 (0x80042306).

## 参考資料

VMware Converter の使用とトラブルシューティングに関するベスト プラクティス

<http://kb.vmware.com/selfservice/documentLinkInt.do?micrositeID=&popup=true&languageId=&externalID=1033253>

公式サイトのサポートページです。

<http://www.vmware.com/support/converter/doc/releasenotes_conv40.html>
<http://communities.vmware.com/thread/308014>

公式サイトのフォーラムです。  
エラーが発生した場合は、『VMware (エラーコード)』で検索すると、
手がかりが得られるかも知れません。

