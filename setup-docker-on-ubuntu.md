# Docker環境セットアップ
このドキュメントでは、UbuntuにDocker環境を構築する方法について説明します。

## パッケージリストを更新
```bash
sudo apt update
```

## apt が HTTPS 経由でパッケージを使用できるように必要なパッケージをインストール
```bash
sudo apt install -y ca-certificates curl gnupg
```

## 公式の GPG キーを保存するディレクトリを作成
```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

## 公式の GPG キーを取得
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

## 公式 Docker リポジトリを追加
```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## パッケージリストを再度更新
```bash
sudo apt update
```

## Docker をインストール
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

# sudo 権限なしで Docker コマンドを実行できるように設定
* rootに近い権限を持つため注意
* パブリック環境では非推奨

## 対象のユーザをdockerグループに追加
```bash
sudo usermod -aG docker {USER}
```

# プロキシを設定

## systemd の設定ファイルを開く
```bash
sudo systemctl edit docker
```

## 環境変数に設定
* ドロップインファイルに記述
```bash
[Service]
Environment = "http_proxy={PROXY}:{PORT}" "https_proxy={PROXY}:{PORT}"
```

## 再起動して設定を反映
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```
