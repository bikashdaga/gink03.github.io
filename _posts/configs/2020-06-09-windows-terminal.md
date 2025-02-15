---
layout: post
title: "windows-terminal"
date: 2020-06-09
excerpt: "windows-terminalの使い方"
tags: ["windows-terminal", "windows"]
config: true
comments: false
sort_key: "2022-02-20"
update_dates: ["2022-02-20","2022-02-17","2021-08-22","2021-02-25","2020-11-19","2020-11-18","2020-10-22","2020-10-21","2020-06-09"]
---

# windows-terminalの使い方

## 概要
 - windowsでターミナルを使う際のデファクトスタンダード
   - [プレゼン資料](https://docs.google.com/presentation/d/1gipc9VgBmv98gunpZw16e0MQ_o7dfLkizO7zvFvbBE8/edit?usp=sharing)  

### 動作イメージ

<div align="center">
  <img src="https://user-images.githubusercontent.com/4949982/154488018-ff22b29e-e327-456d-8a2f-3bee30adf5c3.png">
</div>

---

## インストール

```console
> scoop install windows-terminal
```

---

## powershellのカスタマイズ

### starshipのインストール
```console
> scoop install starship vcredist2019
```

### デフォルトプロファイルをnotepadで開く

```shell
if (!(Test-Path -Path $PROFILE)) {
    New-Item -ItemType File -Path $PROFILE -Force
}
notepad $PROFILE
```

### notepadに以下の内容を記す

```shell
Clear-Host
Invoke-Expression (&starship init powershell)
```

---

## ショートカットキーの設定

### 設定方法
 - `ctrl + ,`で設定を開く
 - `JSONファイルを開く`を選択

### 使用できるコマンド一覧
 - [Custom actions in Windows Terminal](https://docs.microsoft.com/en-us/windows/terminal/customize-settings/actions#accepted-modifiers-and-keys)

### JSONファイルのactionsに追加する

```json
{
    "command": 
    {
        "action": "copy",
        "singleLine": false
    },
    "keys": "ctrl+shift+c"
},
{
    "command": "paste",
    "keys": "ctrl+shift+v"
},
{
    "command": 
    {
        "action": "newTab"
    },
    "keys": "ctrl+t"
},
{
    "command": 
    {
        "action": "moveTab",
        "direction": "backward"
    },
    "keys": "ctrl+shift+["
},
{
    "command": 
    {
        "action": "moveTab",
        "direction": "forward"
    },
    "keys": "ctrl+shift+]"
},
{
    "command": 
    {
        "action": "nextTab"
    },
    "keys": "ctrl+]"
},
{
    "command": 
    {
        "action": "prevTab"
    },
    "keys": "ctrl+["
},
{
    "command": 
    {
        "action": "closeTab"
    },
    "keys": "ctrl+w"
},
{
    "command": "find",
    "keys": "ctrl+shift+f"
}
```

---

## トラブルシューティング

### 謎のクラッシュ時の対応
 - windows-terminalをMicrosoft Storeから最新版に更新する  

### おすすめフォント設定
 - フォント
   - [sfmono-square](https://github.com/delphinus/homebrew-sfmono-square)
     - macでビルドして持ってくる必要がある
 - フォント設定
   - `テキストのアンチエイリアシング` -> `ClearType`
 - 配色
   - `Campbell`

---

## 参考
 - [Windowsでイケてるターミナル環境を構築する](https://zenn.dev/nekocodex/articles/c94ae757119b87)
