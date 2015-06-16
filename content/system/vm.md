+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T18:15:26+09:00"
title = "VM作成とVMの初期設定について"

+++

### 1.VM作成

フォームからVMの貸し出し申請後、以下のurlからVM作成を行うことができます。  
[https://ie.u-ryukyu.ac.jp/internal/host-regist/](https://ie.u-ryukyu.ac.jp/internal/host-regist/)

![host-regist](img/system/host-regist1.jpg)

**＊VM作成の権限が付与されるまで「新規VM作成」は表示されません。**  
右に新規VM作成フォームが表示されます。

![host-regist](img/system/host-regist2.jpg)

- 仮想マシン名、ホスト名は適宜入力、OS、CPU、メモリは選択項目から選んでください。
- 使用者名、使用者（uid）、使用者メールアドレスが正しいか確認してください。

＊MXレコードはメールサーバを構築する場合等にチェックしてください。  
＊MXレコードと備考欄以外は必須項目です。

「ok」を押すとVM作成が始まります。  
VM作成には３～５分ほどかかりますで、そのままでお待ちください。

### 2.VMの状態確認

作成したVMの状態をブラウザ上で確認をすることができます。  
左のメニューから作成したVMを選びます。

![host-regist](img/system/host-regist3.jpg)


この画面ではVM作成時の情報を見ることができます。  
また、VMが起動しているかどうかの確認もでき、パワーオン、オフの切り替えを行うことができます。

### 3.VMにインストールされたOSへのアクセス

VM上のOSにアクセスするためにはsshを使います。  
別途メールでお知らせした ie-user というユーザを使いSSHを行います。
```
> ssh -l ie-user [登録したホスト名またはIP]
or
> ssh ie-user@[登録したホスト名またはIP]
```
です。

root で作業したい場合には、
```
> sudo -
or
> sudo -s
```
とします。
以後、新規ユーザを追加するか、または、ie-user のパスワードを変更してください。  
（セキュリティ上、初期のパスワードを使い続けるのは望ましくないため）

なお、VM上のOSは、デフォルトでは学科内からのみsshアクセスを許可しています。  
アクセス制限を変更したい場合は、
```
/etc/hosts.{allow|deny}
```
の設定を変更して下さい。

もし、上記の変更前に学科外からアクセスする必要がある場合は、  
学科外からsshアクセスするためのサーバーが用意されていますので、  
そちらを経由してsshアクセスして下さい。  
学科sshアクセスサーバー: yomitan.ie.u-ryukyu.ac.jp (133.13.48.20)  
(yomitanにsshアクセスするためのユーザーID/Passwordは学科システムのユーザーID/Passwordです)

### 4.学科システムのLDAP認証を利用したい場合

学科のLDAPサーバーを使って認証したい場合は、
```
/etc/nsswitch.conf
```
を、
```
/etc/nsswitch.conf-ieldap
```
に置き換えて下さい。  
また、
```
/etc/pam.d/system-auth
```
を、
```
/etc/pam.d/system-auth-ieldap
```
に置き換えて下さい。

```
nsswitch.conf-ieldap
```
及び、
```
system-auth-ieldap
```
は、学科LDAPサーバーを使った認証のための設定が追加されています。

なお、LDAPクライアントの設定は、
```
/etc/ldap.conf
```
です。

### 5.初期起動サービスについて

VMに初期インストールされているOSは、デフォルトでは殆どのサービスの  
自動起動を停止しています。
```
/sbin/chkconfig –list | grep :on
```
としてみて下さい。

各種サービスを構築したりする場合は、必要に応じて、
```
/sbin/chkconfig httpd on (httpdを自動起動したい場合)
```
などとしてサービスの自動起動設定をして下さい。

以上が貸し出されたVMを使い始める際に役立つと思われる説明です。
以後は使用者が自由にサーバを構築してください。

### 6.パスワードについて

VMのパスワードの変更をする際には以下の条件に沿って設定してください。  
（エラーが出力されます）

- 最低文字数は8文字であること
- 大文字が1文字以上入っていること
- 小文字が1文字以上入っていること
- 記号が1文字以上入っていること
- 数字が1文字以上入っていること

以上です。

### 7.お問い合わせ

VM利用その他学科システムに関するお問い合わせは、

[sys-admin@ie.u-ryukyu.ac.jp](mailto:sys-admin@ie.u-ryukyu.ac.jp)
までお願いします！
