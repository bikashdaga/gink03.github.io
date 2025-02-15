---
layout: post
title: "WSL(Windows Subsystem for Linux)"
date: "2021-10-25"
excerpt: "WSL(Windows Subsystem for Linux)の使い方"
project: false
config: true
tag: ["windows", "linux", "wsl", "Windows Subsystem for Linux"]
comments: false
sort_key: "2022-05-22"
update_dates: ["2022-05-22"]
---

# WSL(Windows Subsystem for Linux)の使い方

## 概要
 - WindowsでLinuxのコマンドをOSと密に連携して操作するシステム
   - WSL1ではnativeで動作していたが、WSL2では仮想マシンベースになった
 - Linux側のVMのターミナルからWindowsのバイナリを実行できたり、Windows側からLinuxのバイナリを実行できる

## ユースケース毎の使い方

### インストール

管理者権限にて

```console
> wsl --install
```

### インストール可能なディストリビューション一覧

```console
> wsl --list --online
```

### ディストリビューションのインストール

#### CUIからディストリビューションのインストール

```console
> wsl --install -d Ubuntu # Ubuntuの場合
> wsl --install -d Debian # Debianの場合
```

#### Microsoft Storeからディストリビューションのインストール
 1. `Microsoft Store`を起動
 2. Ubuntuなどディストリビューション名で検索
 3. ディストリビューション名のアプリを実行しusernameとpasswordを設定して完了


### インストールされたディストリビューションの一覧

```console
> wsl -l
```

### ディストリビューションを指定して起動

```console
> wsl -d Debian
```
 - `Debian`を指定してインストールする場合

### デフォルトのディストリビューションを設定する

```console
> wsl --setdefault Debian
```
 - `Debian`をデフォルトに設定

### インストールされたディストリビューションの削除

```console
> wsl --unregister <distribution-name>
```

### ディストリビューションの仮想マシンを初期状態に戻す
 - 手順
   1. `設定` -> `アプリ` -> `インストールされているアプリ` -> Linuxのパッケージ名で検索 -> `詳細オプション` -> `リセット`
   2. リセット後にLinuxのパッケージ名のアプリを実行することで作り直すことが可能 
 - 参考
   - [グチャグチャになった「Ubuntu on WSL2」のやり直し方/Qiita](https://qiita.com/PoodleMaster/items/b54db3608c4d343d27c4)
 

### wslサービスの再起動

**管理者のpowershellにて**  
```console
> Get-Service LxssManager | Restart-Service
```

### Windowsのファイルシステムへのアクセス
 - `/mnt/<dirve-letter>`のパスにマウントされる
 - Windows側のホームディレクトリは`/mnt/c/Users/<username>`となる
 - OneDriveを利用している場合、Windowsのデスクトップパスは`/mnt/c/Users/<username>/OneDrive/デスクトップ`となる


### wslの中でdockerを利用する
 - `Docker Desktop for Windows`がインストールされてwsl2 integrationが設定されていれば、wslの内部でもdockerコマンドが利用可能になる

---

## 参考
 - [Configure Linux distributions](https://docs.microsoft.com/en-us/windows/wsl/wsl-config)

---

## トラブルシューティング

### ubuntuが日本語化されない

```console
$ sudo apt install language-pack-ja
$ sudo update-locale LANG=ja_JP.UTF8
```

### 起動が極端に遅い
 - 原因
   - なんらかOSの不整合
 - 対応
   - 最新の更新をインストールして再起動

### 起動時にwindowsのファイルシステムのマウントに失敗する
 - 原因
   - なんらかOSの不整合
 - 対応
   - 最新の更新をインストールして再起動

### `bash`でwslが起動しない
 - 原因
   - 不明
 - 対応
   - `> wsl -d Debian`等直接イメージを選択することで起動可能
