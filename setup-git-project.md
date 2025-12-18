## Gitプロジェクト セットアップ
このドキュメントでは、Gitプロジェクトの初期設定を行う方法について説明します。

### Git インストール

#### Mac
* デフォルトでインストールされていない場合のみインストール
```bash
brew install git
```

#### Windows
* Git for Windows を公式サイトからダウンロード、インストール

### ユーザ設定
```sh
git config --global user.name "{username}"
git config --global user.email {email}
```

### 設定一覧を確認
```sh
git config --global --list
```

### リモートリポジトリの作成
* GitHub/GitLabで作成

### ローカルリポジトリの作成

#### ローカルに既存ソースがない場合
```sh
git clone {repository url}
```
* コマンドを実行したディレクトリ内にリポジトリ名のプロジェクトディレクトリが作成 workspace/repository

#### ローカルに既存ソースがある場合
```sh
git init
git remote add origin {repository url}
```
* プロジェクトディレクトリ内で実行 workspace=repository

## その他の設定

### デフォルトのエディタ操作をVSCodeに待機モードで設定
* ```git commit``` や ```git tag -a``` などのエディタ操作が必要な際にVSCodeで起動
* 待機モードによってウィンドウを閉じるまで待機状態となる
```sh
git config --global core.editor "code --wait"
```

### デフォルトのプルをリベース型に設定
```sh
git config --global pull.rebase true
```
