---
layout: post
title: "Octopressのインストール（前編）"
published: true
date: 2012-04-23 12:47
comments: true
tags: Octopress
categories: 
---

OctopressとGitでブログを作ろう、と思い立ってから１週間。  
試行錯誤の末に、ようやくブログが上げられたので、ハマったポイントを紹介してみたいと思います。

インストール環境は、mac OSX Lion + zsh。Xcodeは入ってるところからスタートしました。  
記事内で、ちらっとUbuntuでのインストールにも触れます。関係ない人はスルーで。

![Octocatに似たデザインのmac](https://www.evernote.com/shard/s75/sh/1c5fcc0f-7c94-45ba-9f7d-c9c6909bdfb6/a28bb5b09a4b9d7cc11c78e691395ddd/res/0e3d3046-3527-4e16-bc47-53ff68a3a9df/mac_ball-20120423-205850.jpg.jpg)
## Octopress導入まで

あまり何もないところから、Octopressを導入するところまでの
手順を、ここにまとめてみます。  
大まかに、Octopressインストールまでには、以下のものが必要です。  

1. Ruby 1.9.2以上（1.9.2そのものがおすすめ）
2. Git

オイラのMacに入っていたRubyは1.8.7だったので、  
Ruby-1.9.2を別途入れる必要がありました。
コマンドラインで`ruby --version`と入力して、"1.9.2"と表示されなかった方は、RVMを入れる必要があります。

## Rubyのインストール準備

 [Octopress公式サイト](http://octopress.org/docs/setup/)では、RVMかrbenvで、Rubyをバージョン管理することを勧めています。  
ここでは、RVMを使って進めます。  

突然ですが、質問です。  
あなたのOSはMacですか？  
Yesの方は、RVMのインストールに進んで下さい。  
Noの方。Linuxをお使いで、Curlが入っていない方は、Curlをインストールしないといけません。

### Curlのインストール
Ubuntuの場合は、以下のコマンドでcURLをインストールします。
`sudo apt-get install libcurl-dev`
以上。

<h3 id="rvm_install">RVMのインストール</h3>
次に、どなたさまもこのコマンドを、ターミナルで実行します。ディレクトリは、初期状態で構いません。
`bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)`

ここから、シェルに何を使っているかで、二手に分かれます。  
何のことかわからない方は、最初の道を選んでください。あなたはbash組です。

---
#### 1. bashを使っている方、何のこと？の方
以下のコードを、ターミナルで実行します。


    echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile
    source ~/.bash_profile

#### 2. zshを使っている方
オイラも、今回を機にzshデビューしました。このコードをどうぞ。


    echo '[[ -s $HOME/.rvm/scripts/rvm ]] && source $HOME/.rvm/scripts/rvm' >> ~/.zshrc
    source ~/.zshrc`

---

これで、Rubyを入れる準備ができました。まだ先は長いです。  
でもげっそりしないで下さいね。  
ひとつひとつは大した事じゃないです。うまくいけば・・・  

<h3 id="gcc_install">GCCのインストール </h3>
オイラがインストールを試した中で、一番のポイントは、このGCCでした。  
公式サイトにも載ってない落とし穴なので、注意して読んで下さい。  
シチュエーション別に解説します。  

---
#### 1. Macの方

また質問ですが、あなたのOSはLionですか？   
Noの方は、ここでは何もしなくていいです。RVMのインストールに進みます。  

Yesの方は、ここ（→[GCC-10.7.pkg](https://github.com/downloads/kennethreitz/osx-gcc-installer/GCC-10.7-v2.pkg) ）からインストーラをダウンロードして実行します。

そして環境変数CCをシェルのプロファイルに書き込みます。  
例によって、どちらのシェルを使っているかで、手順が分かれます。  

---
#### bashの方＋なんだか分からない方
`export CC=/usr/bin/gcc-4.2`を、~/.bash_profileに追記し（ファイルがなければ作る）、ターミナルを再起動します。  
こんなふうにコマンドで打つと、勝手にファイルを開くか作って書いてくれます。

    echo "export CC=/usr/bin/gcc-4.2" >> ~/.bash_profile

##### zshの方
zshの方は、ファイル名が違います。  
`export CC=/usr/bin/gcc-4.2`を、`~/.zprofile`に追記してください。  

##### 参考資料：  
[MacOSX LionでのRubyの扱い方、またはllvm-gccについて][Lion_Ruby]  
[FIX for Lion's posix_spawn_ext.bundle: \[BUG\] Segmentation fault][FIX_posix_spawn]


---

#### Ubuntuの方
UbuntuではGCCが入ってないので、build-essentialというライブラリをapt-getして下さい。  
詳しくはリンク先：thincaさんのページを参照。

##### 参考資料：
[Ubuntu のデフォルトでは gcc でコンパイルできないので build-essential を入れておく][Ubuntu_build-essential]

詳しくないので、その他のディストリビューションの事はわかりません。

---

## Rubyのインストール
やっとここまで来ました。
ここからは、手順としてはもう少しです。
PCに頑張ってもらう感じになります。

Rubyをインストールします。
今回必要なライブラリは1.9.2です。
新し過ぎても面倒がある感じなので、スバリ1.9.2そのものをおすすめします。


    rvm install 1.9.2 && rvm use 1.9.2
    rvm rubygems latest


このコマンドで、Rubyのソースコードをダウンロードしながら、  
自動的にコンパイルします。ここでさっきのGCCを使うんです。  
けっこう時間がかかります。


## Gitのインストール
Gitのインストールは、`brew install git`とかやってください。
Ubuntuの方は、`sudo apt-get install git-core`です。

##### 参考資料：
[MacにHomebrewをインストールする（ついでにGitも][Homebrew_insgall]
[せっかちな人のための git 入門 – githubt をインストールし、共同で開発できる環境を整えるまで : 僕は発展途上技術者][git_install]
[最速で Git を Mac にインストールして基本的なコマンドを使う方法][git_install_mac]

---
## 次回
[次回][next]は、いよいよOctopressをインストールします。


[next]: http://satrex.github.com/blog/2012/04/23/installed-octopress-002/
[Lion_Ruby]: http://d.hatena.ne.jp/holypp/20120212/1328992440
[FIX_posix_spawn]: https://gist.github.com/1104557


[Ubuntu_build-essential]: http://thira.plavox.info/blog/2008/10/ubuntu_gcc_buildessential.html


[Homebrew_insgall]: http://d.hatena.ne.jp/STAR_ZERO/20110815/1313416152
[git_install]: http://blog.champierre.com/670  
[git_install_mac]: http://weble.org/2011/02/14/git-mac-install 


