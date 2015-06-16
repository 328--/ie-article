+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T12:01:17+09:00"
title = "Mac OS X について"

+++

### Tips

- アプリケーションの強制終了  
  「command + option + esc」で、強制終了したいアプリケーションを選択  
- プロセスの強制終了  
  ユーティリティの中のアクティビティモニタから、終了したいプロセスを選択  
- 終了・再起動・スリープのダイアログ表示  
  「control + ⏏(CD排出ボタン)」
- シャットダウン  
  「control + command + option + ⏏」
- 再起動  
  「control + command + ⏏」
- スリープ  
  「command + option + ⏏」
- CDから起動  
  Cキーを押しながら、起動
- CDなどの強制排出  
  右クリックしながら、起動
- Shell  
  使用しているシェルの確認・変更
```
 % echo $SHELL
```
 とすることで現在使っているシェルが表示されます。
 ログインシェルを変更するには以下のようにします。以下の例ではtcshに変更しています。

```
 % chsh -s /bin/tcsh
```

- 設定ファイル

[tcshの設定ファイル(.tcshrc)の書き方](system/tcsh)

[zshについて](system/zsh)

 　

## 学内告知掲示板
- [news-ie](https://ie.u-ryukyu.ac.jp/news-ie)
情報工学科の生徒なら、最低でも一日一回は確認しないといけないもの

### Application
#### editor

- [viについて](system/vi)
- [emacsについて](system/emacs)

#### iCal
![iCal](img/system/ical1.jpg)

[iCalについて](system/ical)

