## uv 環境セットアップ
このドキュメントでは、パッケージ管理ツール uv を使用して、Python の仮想環境を構築する方法について説明します。

### uv のインストール
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### uv のバージョン確認
* インストール後にシェルを再起動して以下のコマンドを実行
```sh
uv --version
```

### uv の更新
* 公式インストーラでインストールした場合は、以下のコマンドにより更新可能
```sh
uv self update
```

### uv プロジェクトのセットアップ

#### ローカルに既存ソースがない場合
```sh
uv init --package {project name}
```
* コマンドを実行したディレクトリ内にプロジェクトディレクトリが作成 workspace/project
* `--package` を付けると、Python パッケージとして扱うための構成（`src` 配下のパッケージ構成や、後続のビルド・インストール向けの前提）が整うため、基本的にはこの形を使うとよい

#### ローカルに既存ソースがある場合
```sh
uv init --package
```
* プロジェクトディレクトリ内で実行 workspace=repository
* 既存ソースがある場合は以下のファイルが作成されない可能性があるため注意
  - main.py
  - .gitignore
  - README.md

### Python バージョンの固定
* .python-version ファイルがあり、バージョンが確認できれば実行不要
```sh
uv python pin 3.14
```

### 仮想環境の作成
```sh
uv venv
```

### 依存関係の管理の追加

#### パッケージの追加
```sh
uv add {package name}
```

#### 開発用パッケージの追加
```sh
uv add --dev {package name}
```

#### パッケージの削除
```sh
uv remove {package name}
```

### コマンドの実行
```sh
uv run {command}
```

### 依存関係の同期
* 依存関係の初回インストール時や更新時に実行
```sh
uv sync
```

## ディレクトリ構成例
```
project-name/
├── README.md
├── LICENSE
├── .gitignore
├── pyproject.toml
├── uv.lock
├── .python-version
├── .venv/
│
├── src/
│   └── project_name/
│       ├── __init__.py
│       ├── main.py
│       └── module.py
│
└─ tests/
    ├── __init__.py
    └── test_module.py
```