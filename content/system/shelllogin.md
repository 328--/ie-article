+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T13:41:12+09:00"
title = "サーバアクセス方法(shell login)"

+++

#### sshでログイン

1. Terminalを起動し、以下のコマンドを入力し実行する。（通常はEnterキーを押す）
```
$ ssh e1157XX@shell.ie.u-ryukyu.ac.jp [Enter]
```
コマンドの例における$は、コマンドが入力できる状態であることを示すために表示された文字で、「プロンプト」と呼ばれる。プロンプトは場合によって異なるがここでは$を用いている。
2. パスワードの入力が求められるので、総合情報処理センターより渡されたパスワードを入力する。
sshによるログインの説明は以上です。

#### 学科外からのアクセス
shell.ie.u-ryukyu.ac.jpを起点に学内のサーバにアクセスできます。

また、公開鍵暗号方式を用いたログインでwww.ie.u-ryukyu.ac.jpにもアクセスできます。

#### 公開鍵暗号方式を用いたログイン
より安全な、公開鍵暗号方式を用いたログイン方法について説明する。


1. ローカル（手元）のコンピュータ上で秘密鍵と公開鍵を作成する
```
Local$ cd ~ [Enter]
Local$ mkdir .ssh [Enter]
Local$ chmod 700 .ssh [Enter] （自分だけが読み書きできるように）
Local$ ssh-keygen [Enter] （鍵の作成）
Generating public/private rsa1 key pair.
Enter file in which to save the key (/home/foo/.ssh/identity): [Enter]
Enter passphrase (empty for no passphrase): “適当なパスフレーズ” [Enter]（ログインする際に用いる何か適当なフレーズを入力）
Enter same passphrase again: “適当なパスフレーズ” [Enter]（繰り返し）
Your identification has been saved in /home/foo/.ssh/identity.
Your public key has been saved in /home/foo/.ssh/identity.pub.
The key fingerprint is:
aa:aa:aa:aa:aa:aa:aa:aa:aa:aa:aa:aa:aa:aa:aa:aa foo@localhost
```
2. 公開鍵をリモート（ログイン先）のコンピュータに登録する
まず、リモートに公開鍵を送ります。
```
Local$ scp ~/.ssh/id_rsa.pub e1157XX@shell.ie.u-ryukyu.ac.jp: [Enter]
```

(この時，ホスト名である e1157XX@shell.ie.u-ryukyu.ac.jp の後ろにある「:」まで入力して下さい．)
さらに、リモートのホスト側で登録作業を行います。

```
Local$ ssh e1157XX@shell.ie.u-ryukyu.ac.jp [Enter]
Remort$ mkdir .ssh[Enter]
Remort$ chmod 700 .ssh/[Enter] （自分だけが読み書きできるように）
Remort$ cd .ssh/
Remort$ touch authorized_keys[Enter] （公開鍵登録用のファイルを作成）
Remort$ chmod 600 authorized_keys[Enter] （自分だけが読み書きできるように）
Remort$ cat ~/id_rsa.pub >>authorized_keys[Enter] （公開鍵の登録）
Remort$ rm ~/id_rsa.pub[Enter] （いらなくなった鍵を削除）
```

秘密鍵の管理には注意してください。

特に、パスフレーズを入力しないで鍵を作成するとパスフレーズ無しでログイン出来ますが、セキュリティー上の影響を考慮しましょう。

パスワードを打つのが手間だと感じる方は、ssh-agentなどを使用してセキュリティを犠牲にせずに、パスワードレスの認証を行う方法を用いましょう。
