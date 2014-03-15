---
layout: post
title: "bitbucketへ引っ越してみた"
published: true
date: 2012-05-08 20:59
comments: true
tags: 
categories: octopress 
---

ブログのリポジトリを、githubからbitbucketへ移してみました。
だんだんGitの使い方に習熟してきたので、楽になってきました。

## 下書きモード

octopressの取り扱いに慣れるため、published=falseの下書きモードを使ってみています。
記事のヘッダーのpublished:をfalseに設定することで、その記事は下書きとなります。
ローカルでプレビューすることができるのはpublish:trueの時と同じですが、リポジトリにpushしても非公開になっているところが違います。

## 使い道について考えてみた

ローカルのプレビューができれば、下書きモードのpushはあまり恩恵がないような気がしますが・・・
どんな時に便利なんでしょうか。

タイマーで予約投稿ができれば便利な気がします。

## その後

結局、bitbucketは記事のソースだけを管理することにし、
記事はgithub pagesを使う事にしました。

理由は、bitbucketは**CNAMEが有料オプション**だからです。
画像はSkitchに置くことにし、Skitchから効率よくMarkdownに書けるように
工夫します。

