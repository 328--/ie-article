+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T12:39:17+09:00"
title = "emacs"

+++


### emacsとは
Emacs（イーマクス）とは、テキストエディタの種類の1つである。 高機能でカスタマイズ性の高いプログラマ向けスクリーン・エディタとして、viに並び、UNIXのプログラマを中心としたコンピュータ技術者に人気がある

　

### emacsの使い方
- 編集開始
```
% emacs -nw ファイル名
```
- 保存
```
 C-x C-s
```
(control 押しながら x 押した後, control 押しながら s )

- 終了
```
C-x C-c
```

### emacsの設定

- emacsで文字コード(UTF-8)を指定する
設定ファイル（~/.emacs）を以下のように変更
```
;; 日本語の設定
(set-language-environment "Japanese")
(prefer-coding-system 'utf-8)
(set-default-coding-systems 'utf-8)
(set-terminal-coding-system 'utf-8)
(set-keyboard-coding-system 'utf-8)
(set-buffer-file-coding-system 'utf-8)
(setq default-buffer-file-coding-system 'utf-8)
(set-buffer-file-coding-system 'utf-8)
(set-clipboard-coding-system 'utf-8)
(utf-translate-cjk-mode t)
```
　

- その他の設定

以下の設定は、あるとちょっと便利になる程度の設定
```
;; それぞれの色を設定する
(set-cursor-color "ForestGreen")   ;; マウスカーソル
(set-background-color "black")     ;; 背景色
(set-foreground-color "snow")      ;; 文字色
(set-face-foreground 'fringe "snow")       ;; 両脇のバーの文字色
(set-face-background 'fringe "dark red")   ;; 両脇のバーの背景色
(set-face-foreground 'mode-line-inactive "white")  ;; アクティブでないバッファの文字色
(set-face-background 'mode-line-inactive "MediumPurple4")  ;; アクティブでないバッファの背景色

;; 選択範囲に色を付ける
(setq transient-mark-mode t)
(set-face-foreground 'region "black")
(set-face-background 'region "PaleGreen")

;; 全角スペースやタブ文字、行末のスペースを色を付けて表示する
(global-font-lock-mode t)
(defface my-face-b-1 '((t (:background "gray"))) nil)
(defface my-face-b-2 '((t (:background "gray26"))) nil)
(defface my-face-u-1 '((t (:foreground "SteelBlue" :underline t))) nil)
(defvar my-face-b-1 'my-face-b-1)
(defvar my-face-b-2 'my-face-b-2)
(defvar my-face-u-1 'my-face-u-1)
(defadvice font-lock-mode (before my-font-lock-mode ())
  (font-lock-add-keywords
   major-mode
   '(("¥t" 0 my-face-b-2 append)
     ("　" 0 my-face-b-1 append)
     ("[ ¥t]+$" 0 my-face-u-1 append)
     )))
(ad-enable-advice 'font-lock-mode 'before 'my-font-lock-mode)
(ad-activate 'font-lock-mode)

;; -*- ここからの設定は Carbon Emacs(Emacs.app)で使うやつ -*-
;; 日本語の表示が崩れないようにする
(when (eq window-system 'mac)
;; 日本語フォントにヒラギノを使う
(set-fontset-font nil 'japanese-jisx0208 '("ヒラギノ角ゴ*" . "jisx0208.*"))
(set-fontset-font nil 'katakana-jisx0201 '("ヒラギノ角ゴ*" . "jisx0201.*"))
;; 日本語フォントの幅をASCIIの倍に調整(たいがいはこれでOK)
(setq face-font-rescale-alist '(("-jisx02[^-]*-[^-]*¥¥'" . 1.2)))
;; 日本語フォントのboldに重ね打ちを使う(幅が変わらない)
(setq face-ignored-fonts '("¥¥`-[^-]*-[^-]*-bold-.*-jisx02[^-]*-[^-]*¥¥'"))
)

;; フレームサイズと位置の指定
(setq initial-frame-alist
      (append
       '((top . 0)       ;; フレームの Y 位置(ピクセル数)
         ;(left . 600)   ;; フレームの X 位置(ピクセル数)
         (width . 95)    ;; フレーム幅(文字数)
         (height . 45)   ;; フレーム高(文字数)
       initial-frame-alist))
```
