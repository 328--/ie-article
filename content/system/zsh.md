+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T12:17:07+09:00"
title = "zsh"

+++

### zshとは？

tcsh同様の、Unixのシェルである。
本学科では最初tcshを導入するが、zshにはいろいろな便利な機能があるため、あとでtcshからzshに移る人も多い。

zshはMac OS Xでは最初からインストールされているため、
```
chsh -s /bin/zsh
```
を実行するだけで、デフォルトのシェルをzshに変えることが出来る。

### zshの設定ファイル（.zshrc）の書き方

- サンプル
[グッバイ野郎ども! コピペではじめるzshファイナル](http://news.mynavi.jp/column/zsh/024/)


- 文字コードの設定
「ls /usr/share/locale/」で表示されるもののなかから選びます
```
#!/bin/zsh
export LANG=ja_JP.UTF-8
case ${UID} in
0)
    LANG=C
        ;;
esac
```

- 色付プロンプトの設定
```
## Default shell configuration
# set prompt
autoload colors
colors
case ${UID} in
0)
    PROMPT="%{${fg[cyan]}%}$(echo ${HOST%%.*} | tr '[a-z]' '[A-Z]') %B%{${fg[red]}%}%/#%{${reset_color}%}%b "
    PROMPT2="%B%{${fg[red]}%}%_#%{${reset_color}%}%b "
    SPROMPT="%B%{${fg[red]}%}%r is correct? [n,y,a,e]:%{${reset_color}%}%b "
    ;;
*)
    PROMPT="%{${fg[red]}%}%/%%%{${reset_color}%} "
    PROMPT2="%{${fg[red]}%}%_%%%{${reset_color}%} "
    SPROMPT="%{${fg[red]}%}%r is correct? [n,y,a,e]:%{${reset_color}%} "
    [ -n "${REMOTEHOST}${SSH_CONNECTION}" ] && 
        PROMPT="%{${fg[cyan]}%}$(echo ${HOST%%.*} | tr '[a-z]' '[A-Z]') ${PROMPT}"
    ;;
esac
```

- パスの補完や、パスを自動的に記録しcd – [tab]でこれまでで記録したパスが補完表示される設定など
```
# auto change directory
setopt auto_cd
# auto directory pushd that you can get dirs list by cd -[tab]
setopt auto_pushd
# command correct edition before each completion attempt
setopt correct
# compacked complete list display
setopt list_packed
# no remove postfix slash of command line
setopt noautoremoveslash
# no beep sound when complete list displayed
setopt nolistbeep
```


- Emacs風のショートカットキー設定など
```
bindkey -e
bindkey "^[[1~" beginning-of-line # Home gets to line head
bindkey "^[[4~" end-of-line # End gets to line end
bindkey "^[[3~" delete-char # Del
```

- コマンド履歴の有効化と検索用のショートカットの設定
```
# historical backward/forward search with linehead string binded to ^P/^N
autoload history-search-end
zle -N history-beginning-search-backward-end history-search-end
zle -N history-beginning-search-forward-end history-search-end
bindkey "^p" history-beginning-search-backward-end
bindkey "^n" history-beginning-search-forward-end
bindkey "\\ep" history-beginning-search-backward-end
bindkey "\\en" history-beginning-search-forward-end
# reverse menu completion binded to Shift-Tab
bindkey "\e[Z" reverse-menu-complete
## Command history configuration
HISTFILE=${HOME}/.zsh_history
HISTSIZE=50000
SAVEHIST=50000
setopt hist_ignore_dups     # ignore duplication command history list
setopt share_history        # share command history data
```

- コマンド補完ファイルを置いておくディレクトリを指定
```
## Completion configuration
fpath=(${HOME}/.zsh/functions/Completion ${fpath})
```

- 強力な補完機能の有効化
```
autoload -U compinit
compinit
```

- zshのエディタ機能zedの有効化
```
## zsh editor
autoload zed
```

- aliasの設定。
aliasとは長いコマンドに別名を与えて簡単に使えるようにすること。
```
## Alias configuration
# expand aliases before completing
setopt complete_aliases     # aliased ls needs if file/dir completions work
alias where="command -v"
alias j="jobs -l"
case "${OSTYPE}" in
freebsd*|darwin*)
    alias ls="ls -G -w"
    ;;
linux*)
    alias ls="ls --color"
    ;;
esac

alias la="ls -a"
alias lf="ls -F"
alias ll="ls -l"
alias du="du -h"
alias df="df -h"
alias su="su -l"
```
- ls色付け、補完候補に色付け、ターミナルタイトルにパスを表示
```
## terminal configuration
case "${TERM}" in
screen)
    TERM=xterm
    ;;
esac

case "${TERM}" in
xterm|xterm-color)
    export LSCOLORS=exfxcxdxbxegedabagacad
    export LS_COLORS='di=34:ln=35:so=32:pi=33:ex=31:bd=46;34:cd=43;34:su=41;30:sg=46;30:tw=42;30:ow=43;30'
    zstyle ':completion:*' list-colors 'di=34' 'ln=35' 'so=32' 'ex=31' 'bd=46;34' 'cd=43;34'
    ;;
kterm-color)
    stty erase '^H'
    export LSCOLORS=exfxcxdxbxegedabagacad
    export LS_COLORS='di=34:ln=35:so=32:pi=33:ex=31:bd=46;34:cd=43;34:su=41;30:sg=46;30:tw=42;30:ow=43;30'
    zstyle ':completion:*' list-colors 'di=34' 'ln=35' 'so=32' 'ex=31' 'bd=46;34' 'cd=43;34'
    ;;
kterm)
    stty erase '^H'
    ;;
cons25)
    unset LANG
    export LSCOLORS=ExFxCxdxBxegedabagacad
    export LS_COLORS='di=01;34:ln=01;35:so=01;32:ex=01;31:bd=46;34:cd=43;34:su=41;30:sg=46;30:tw=42;30:ow=43;30'
    zstyle ':completion:*' list-colors 'di=;34;1' 'ln=;35;1' 'so=;32;1' 'ex=31;1' 'bd=46;34' 'cd=43;34'
    ;;
jfbterm-color)
    export LSCOLORS=gxFxCxdxBxegedabagacad
    export LS_COLORS='di=01;36:ln=01;35:so=01;32:ex=01;31:bd=46;34:cd=43;34:su=41;30:sg=46;30:tw=42;30:ow=43;30'
    zstyle ':completion:*' list-colors 'di=;36;1' 'ln=;35;1' 'so=;32;1' 'ex=31;1' 'bd=46;34' 'cd=43;34'
    ;;
esac
# set terminal title including current directory
case "${TERM}" in
xterm|xterm-color|kterm|kterm-color)
    precmd() {
        echo -ne "\033]0;${USER}@${HOST%%.*}:${PWD}\007"
    }
    ;;
esac
```
- パスを通します、パスが通ったところにあるコマンドやプログラムはどのディレクトリにいても使えます
```
path = (/usr/local/bin $path)
path = ($path /usr/X11R6/bin/usr/local/ws/bin)
path = ($path . ~/bin)
path = ($path /Developer/Tools)
path = ($path /usr/local/mysql/bin)
```
- ブロンプトの設定です、以下は「[ユーザ名:今いるディレクトリ（絶対パス）]%」と表示
```
prompt = '[%n:%~]%%'
```
他にも様々な機能を持っている。
上記の内容や、それ以外の機能を使いたい場合は検索してみると様々な情報を得ることが出来る。


### 参考
- [漢のzsh](http://journal.mycom.co.jp/column/zsh/index.html)
