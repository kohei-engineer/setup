# プロキシ セットアップ
このドキュメントでは、Ubuntuにプロキシを設定する方法について説明します。

## 環境変数の設定
* 一般的なプロキシ設定ではなく、ログイン時に自動的に適用される永続的な設定

### プロキシの確認方法
```bash
printenv http_proxy https_proxy
```

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
