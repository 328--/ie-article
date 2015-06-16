+++
Categories = []
Description = ""
Keywords = []
Tags = []
date = "2015-06-16T18:27:09+09:00"
title = "VM質問 Tips"

+++

このページでは、学科からVMを借りている人から来る質問をまとめます。

##### Q: sshで接続を行う際、以下のような警告が出てつながらない場合の対応

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the RSA host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
AA:BB:CC:DD:EE:FF:GG:HH:II:JJ:KK:LL:MM:NN:OO:PP.
Please contact your system administrator.
Add correct host key in /home/USERNAME/.ssh/known_hosts to get rid of this message.
Offending key in /home/USERNAME/.ssh/known_hosts:1
RSA host key for HOSTNAME has changed and you have requested strict checking.
Host key verification failed.
```

ログを読むと/home/USERNAME/.ssh/known_hosts:1のせいで繋がらないうことがわかる。
なので/home/USERNAME/.ssh/known_hostsの1行目を消しましょう。

##### Q: “ssh_exchange_identification: Connection closed by remote host”と出て接続できない
学外からサーバにアクセスしていませんか？  
学外からのアクセスは基本的に出来ないようにしてあるので、yomitanなどを経由してログインして下さい。
