+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T12:10:55+09:00"
title = "tcsh"

+++

- サンプル

文字コードの設定です、「ls /usr/share/locale/」で表示されるもののなかから選びます

```
#!/bin/tcsh
setenv LANG ja_JP.UTF-8
setenv LANGUAGE ja_JP.UTF-8
setenv LC_ALL ja_JP.UTF-8
setenv LC_COLLATE C
setenv LC_TIME C
```

- ディスプレイの設定

```
if (! $?DISPLAY) then
  setenv DISPLAY :0.0
endif
```

ブロンプトの設定です、以下は「[ユーザ名:今いるディレクトリ（絶対パス）]%」と表示

```
set prompt = '[%n:%~]%%'
```

- 便利な設定
```
set savehist=50   //５０個前まで使ったコマンドを覚えておく
set autolist  //Tabボタンを押した時に自動補完
set rmster   //rm * した時に、ほんとにやっていいか聞きいてくる
```

以下はaliasといって、ながったらしいコマンドを簡単に使うことができるようにするものです
```
alias ls "gnuls --color=auto -F --show-control-char"
alias platex "platex -kanji=euc"
alias finder "open -a finder"  //finderと入力するとfinderが起動
alias diff "diff -y -W100"
alias showall "defaults write com.apple.finder AppleShowAllFiles TRUE"
```
