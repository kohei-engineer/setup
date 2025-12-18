## WSL環境セットアップ
このドキュメントでは、WSL2環境を構築する方法について説明します。

### WSLのステータス確認
* インストール済みの場合は既定のディストリビューション及びバージョンが表示される
```powershell
wsl --status
```

### WSLをインストール
```powershell
wsl --install
```

### WSLのバージョンを確認
```powershell
wsl --version
```

### ディストリビューションを確認
* ```*```が付いているものが既定のディストリビューション
```powershell
wsl --list --verbose
```

### 既定のディストリビューションの変更
* 既定のディストリビューションを変更したい場合のみ必要
```powershell
wsl --set-default {DistributionName}
```

### インストール可能なディストリビューション一覧を表示
```powershell
wsl --list --online
```

### ディストリビューションのインストール
```powershell
wsl --install -d {DistributionName}
```
* ただし、同じ名前でのディストリビューションのインストールはできないため名前の指定が必要
```powershell
wsl --install -d {DistributionName} --name {Name}
```

### インストール済みのディストリビューション名の変更
```powershell
wsl --rename {DistributionName} {NewDistributionName}
```

### インストール済みのディストリビューションの削除
```powershell
wsl --unregister {DistributionName}
```
