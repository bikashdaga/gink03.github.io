---
layout: post
title: "universal control"
date: 2022-03-24
excerpt: "appleのuniversal control(ユニバーサルコントロール)の使い方"
project: false
config: true
tag: ["apple", "ios", "osx", "universal control"]
comments: false
---

# appleのuniversal control(ユニバーサルコントロール)の使い方

## 概要
 - MacBookとiPadのキーボードとマウスを一体化してシームレスに移動・コントロールする仕組み
 - 簡単なファイルのやり取りをD&Dで行える
 - sidecarやduetなどは遅延が発生するが、キーボードとマウスの移動だけが発生するので軽く、それぞれのデバイスのリソースをフルに使える

## 必要要件
 - 最新のipad os, osx
 - それぞれのデバイスでWiFi, Bluetooth, Handoffが有効になっていること
   - WiFiでで接続する場合、同じサブネットマスクにある必要がある
   - テザリング環境下など通信がうまくできない環境ではUSB接続で通信できる
 - 同じapple idでログインしていること
 - `[システム環境設定]` -> `[ディスプレイ]` -> `[ユニバーサルコントロール]`

## 基本的な使い方
 - iPadからホームに戻る
   - 下のバーをクリック
 - アプリの切り替え
   - MacBookのディスプレイ切り替えと同じタッチパッドのスワイプ
 - コピーアンドペースト
   - できないのでドラッグアンドドロップする

## トラブルシューティング
 - iPadへカーソルが行ったまま帰ってこない
   - 通信が不安定になっていることが原因
   - 一度MacBookを閉じて再度開くと直る
 - WiFi経由でユニバーサルコントロールを行った時マウスが遅延する
   - USBで接続し直すと改善する
 - USB接続でテザリング時にユニバーサルコントロールが開始されない
   - WiFiのイベントと紐付いているらしく、WiFiがONになっている必要がある

## 参考
 - [「ユニバーサルコントロール」を利用する方法](https://applech2.com/archives/20220315-how-to-use-universal-control-macos-123-monterey.html)
 - [Mac ユニバーサルコントロールの使い方と、アップデート方法と、使用感](https://youtu.be/kc71EfsEo5w)