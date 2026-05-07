## .NET (C#) 環境セットアップ
このドキュメントでは、Windows 上で .NET SDK を使って C# プロジェクトの初期設定を行う方法について説明します。

### .NET SDK のインストール
Windows では公式インストーラーか winget コマンドを使用
* SDK のバージョンは LTS を確認してインストール
```sh
winget install Microsoft.DotNet.SDK.8
```

### .NET SDK のバージョン確認
* インストール後にシェルを再起動して以下のコマンドを実行
```sh
dotnet --version
dotnet --list-sdks
```

### .NET SDK のアンインストール
Windows では公式インストーラーか winget コマンドを使用
* SDK のバージョンは LTS を確認してインストール
```sh
winget uninstall Microsoft.DotNet.SDK.{version}
```

### プロジェクトのセットアップ
```sh
mkdir ProjectName
cd ProjectName
dotnet new console
```

### プロジェクトの実行
```sh
dotnet run
```

### プロジェクトの配布
```sh
dotnet publish -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -p:IncludeNativeLibrariesForSelfExtract=true -p:DebugType=None -p:DebugSymbols=false
```
* コマンド実行後、実行ファイルは ```bin\Release\net{version}\win-x64\publish\``` を参照

## ディレクトリ構成例
```
ProjectName/
├── ProjectName.csproj
├── Program.cs
├── bin/
└── obj/
```
