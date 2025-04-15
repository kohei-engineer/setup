# 仮想サーバへの接続
このドキュメントでは、仮想サーバに接続する方法について説明します。

## シェル

### 指定のアカウントでログイン
- コマンド実行 ```ssh {User}@{IP}```
- パスワード入力

### 管理者アカウントに切替
- コマンド実行 ```su```
- パスワード入力

## vscode

### 指定のアカウントでログイン
- 拡張機能「Remote-SSH」をインストール
- コマンドパレットを展開(Ctrl + Shift + P)
- 「Remote-SSH: Connect to Host」を選択
- 「Configure SSH Hosts」を選択
- 「Users/{User}/.ssh/config」を選択
- 以下の記述を追加
```
Host {IP}
  HostName {IP}
  User {User}
```
- 再度「Remote-SSH: Connect to Host」を選択
- {IP}を選択
- 「Linux」を選択
- {PW}を入力
