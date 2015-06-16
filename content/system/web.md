+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T12:54:55+09:00"
title = "web"

+++

## webサーバ( urasoe )とは

WWWシステムにおいて、情報送信を行なうコンピュータ
このサーバの所定の位置に置いたファイルはインターネットを通して閲覧することが出来る
２４時間稼働している
情報工学科のwebサーバではperlとPHP,Rubyも使用可能。

### webサーバの使い方
www.ie.u-ryukyu.ac.jp内の ~/public_html 以下にファイルを置いてください。
すると「http://www.ie.u-ryukyu.ac.jp/~eXXXXXX/」でページを見ることが出来ます。

### rsyncを使う

rsyncコマンドを使ってノートパソコンからデータを転送することもできます。

```
rsync -auvz -e ssh ~/Sites/ eXXXXXX@ie.u-ryukyu.ac.jp:~/public_html
```

### リモートログインして直接書く

sshでリモートログインしてemacs等を使ってもいいです

```
%ssh eXXXXXX@ie.u-ryukyu.ac.jp

%cd public_html

%emacs -nw index.html
```
