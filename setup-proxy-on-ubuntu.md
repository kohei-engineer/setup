# プロキシ セットアップ
このドキュメントでは、Ubuntuにプロキシを設定する方法について説明します。

## プロキシの確認方法
```bash
printenv http_proxy https_proxy
```

## プロキシの設定箇所の確認方法
```bash
sudo grep -r http_proxy /etc/*
```

## 環境変数の設定(ログインユーザのbash)
* ログインユーザのbashシェルのみを対象とし、ログイン時に自動的に適用される永続的な設定

### .bashrc ファイルを開く
```bash
nano ~/.bashrc
```

### プロキシ設定を追加
* 末尾に追記
```bash
## proxy setting
export http_proxy="{PROXY}:{PORT}"
export https_proxy=$http_proxy
```

### 設定を反映
```bash
source ~/.bashrc
```

## 環境変数の設定(全ユーザのシステムシェル設定)
* 全ユーザのあらゆるシェルを対象とし、ログイン時に自動的に適用される永続的な設定

### proxy.sh ファイルを開く
```bash
nano /etc/profile.d/proxy.sh
```

### プロキシ設定を追加
* 末尾に追記
```bash
# proxy setting
MY_PROXY="{PROXY}:{PORT}"

HTTP_PROXY="$MY_PROXY"
HTTPS_PROXY="$MY_PROXY"
FTP_PROXY="$MY_PROXY"
http_proxy="$MY_PROXY"
https_proxy="$MY_PROXY"
ftp_proxy="$MY_PROXY"

export HTTP_PROXY HTTPS_PROXY FTP_PROXY http_proxy https_proxy ftp_proxy
```

### 設定を反映
* シェルを再起動

## 環境変数の設定(全ユーザのシステム設定)
* 全ユーザの全プロセスを対象とし、ログイン時に自動的に適用される永続的な設定

### environment ファイルを開く
```bash
nano /etc/environment
```

### プロキシ設定を追加
* 末尾に追記
```bash
# proxy setting
http_proxy="{PROXY}:{PORT}/"
HTTP_PROXY="{PROXY}:{PORT}/"
https_proxy="{PROXY}:{PORT}/"
HTTPS_PROXY="{PROXY}:{PORT}/"
ftp_proxy="{PROXY}:{PORT}/"
FTP_PROXY="{PROXY}:{PORT}/"
no_proxy="localhost,127.0.0.1,{DOMAIN}"
NO_PROXY="localhost,127.0.0.1,{DOMAIN}"
```
* {DOMAIN}にサブドメインは含まない

### 設定を反映
* ログインしているセッションを再起動

## apt の設定

### apt.confファイルを開く
```bash
sudo nano /etc/apt/apt.conf
```

### プロキシ設定を追加
```bash
Acquire::http::Proxy "{PROXY}:{PORT}";
Acquire::https::Proxy "{PROXY}:{PORT}";
```
