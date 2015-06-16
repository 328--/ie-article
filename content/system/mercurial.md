+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T13:49:21+09:00"
title = "Mercurial"

+++
Mercurial(マーキュリアル)は、クロスプラットフォームの分散型バージョン管理システムです。

```
yomitan:/home/hg
```
に皆さんのリポジトリ用スペースが用意されています。

ここのリポジトリの内容は[Mercurial閲覧のページ](http://www.ie.u-ryukyu.ac.jp/hg/)で確認することができます。


#### 使い方

まず、EasyPackage.appでMarcurialをあなたのパソコンにインストールしてください。
Homebrewの場合は
```
brew install mercurial
```
次に、yomitan:/home/hg/y0x/e0x57xx/のフォルダをレポジトリとして使用するために、

sshでyomitanに入り、/home/hg/y0x/e0x57xx/のフォルダまで移動し、リポジトリを作成します。

```
ssh e0x57xx@yomitan.ie.u-ryukyu.ac.jp

Password:

[yomitan:~] e0x57xx% cd /home/hg/y0x/e0x57xx/
[yomitan:hg/y0x/e0x57xx] e0x57xx% hg init
```


次に、/home/hg/y0x/e0x57xx/に用意したリポジトリの内容をあなたのパソコンでも編集できるように、

あなたのパソコンにリポジトリを複製します。

ssh経由でhgコマンドを使用するので、あなたのyomitanのホームディレクトリにある.ssh/environmentを編集し（無ければ作成）、ssh経由用にhgのパスを通してあげる必要があります。


```
ssh e0x57xx@yomitan.ie.u-ryukyu.ac.jp

Password:

[yomitan:~] e0x57xx% cd  .ssh

[yomitan:~/.ssh] e0x57xx% emacs -nw environment

//environmentに記入

PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

ssh経由でのhgのパスを通すことができたので、あなたのパソコンで、
```
hg clone ssh://e0x57xx@yomitan.ie.u-ryukyu.ac.jp//home/hg/y0x/e0x57xx [directory name]
```

複製したリポジトリを編集します。


- ディレクトリ、ファイルをレポジトリに追加
```
hg add (file name)
```

- リポジトリに反映させるためにcommit
```
hg commit
```

- リポジトリに反映されていない情報を破棄して、元に戻す。
```
hg revert
```
- 前回のバージョンからの変更されたファイルの確認
```
hg status
```
- 前回のバージョンからの変更されたファイルの変更点の確認
```
hg diff
```
- 作業の更新履歴
```
hg log
```
あなたのパソコンで編集した内容、リポジトリの情報は、/home/hg/y0x/e0x57xx/のリポジトリにはまだ反映されていません。

なので、hg push で/home/hg/y0x/e0x57xx/に反映させ、公開させることができます。
```
hg push
```
と入力することで、/home/hg/y0x/e0x57xx/のリポジトリに情報を反映させることが出来ます。
ただし、このままだと yomitan のワーキングディレクトリは変更されないので、それを表示するには、 yomitan 側の/home/hg/y0x/e0x57xx/で、
```
hg update
```
を実行する必要があります。これで/home/hg/y0x/e0x57xx/の中に変更したファイルが表示される様になります。
また、これを行わない場合バイナリファイル(pdf 等)はMercurial閲覧で見る事ができません。
