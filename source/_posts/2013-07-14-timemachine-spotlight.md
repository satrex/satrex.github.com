---
layout: post
title: "TimeMachineのバックアップが遅い時は、Spotlightを確認せよ"
published: true
date: 2013-07-14 07:39
comments: true
tags: 
categories: 
---

今回は、タイトルで内容を言い尽くした感があります。

### 今回起こったこと

約２週間前から、TimeMachineのバックアップが成功しなくなりました。 
 
夜寝ようとすると、『バックアップ230MB/6GB』とか表示されてるわけです。 
で、InsomniaTを仕掛けてスリープしないようにし、翌朝バックアップが終わったか確認すると・・・　
『バックアップ2.4GB/6GB』 
とか出ているわけです。 

丸一日かかる計算です。
もう仕事に持っていくし、終わんねーじゃん。 
こんな事が数日続いたでしょうか・・・

### Spotlightの異変

仕事中に、ふと気がついた事がありました。 
Spotlightで検索できない。

ぐぐる。
[OSX Daily](http://osxdaily.com/2011/12/10/disable-or-enable-spotlight-in-mac-os-x-lion/) 
[appleのフォーラム](https://discussionsjapan.apple.com/thread/10119501?start=0&tstart=0) 

今回は、下のコマンドで解決できました。

`
sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist
`
　
### TimeMachineも解決したよ

Spotlightが解決したら、TimeMachineのバックアップもうまくいきました。
たまった差分バックアップが9時間で終わった感じですが。

めでたし。
