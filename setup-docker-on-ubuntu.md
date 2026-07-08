## Docker環境セットアップ
このドキュメントでは、UbuntuにDocker環境を構築する方法について説明します。

### パッケージリストを更新
```bash
sudo apt update
```

### apt が HTTPS 経由でパッケージを使用できるように必要なパッケージをインストール
```bash
sudo apt install -y ca-certificates curl
```

### 公式の GPG キーを保存するディレクトリを作成
```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

### 公式の GPG キーを取得

**プロキシ環境がない場合:**
```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

**プロキシ環境がある場合:**
```bash
sudo http_proxy=http://{PROXY}:{PORT} https_proxy=http://{PROXY}:{PORT} curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### 公式 Docker リポジトリを追加
```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

### パッケージリストを再度更新
```bash
sudo apt update
```

### Docker をインストール
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### インストールの確認
```bash
sudo systemctl status docker
```

## sudo 権限なしで Docker コマンドを実行できるように設定
* rootに近い権限を持つため注意
* パブリック環境では非推奨

### docker グループを作成
```bash
sudo groupadd docker
```

### 対象のユーザをdockerグループに追加
```bash
sudo usermod -aG docker $USER
```

### グループ変更を反映
ログアウト後にログインし直すか、次のコマンドで即座に反映：
```bash
newgrp docker
```

### 動作確認
```bash
docker ps
```

## プロキシを設定

### systemd の設定ファイルを開く
```bash
sudo systemctl edit docker
```

### 環境変数に設定
* ドロップインファイルに記述
```ini
[Service]
Environment = "http_proxy={PROXY}:{PORT}" "https_proxy={PROXY}:{PORT}"
```

### 設定を反映
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```
