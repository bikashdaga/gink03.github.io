---
layout: post
title: "Apple AirTags"
date: 2022-04-09
excerpt: "Apple AirTagsについて"
tags: ["apple", "airtags"]
config: true
comments: false
sort_key: "2022-04-09"
update_dates: ["2022-04-09"]
---


# Apple AirTagsについて

## 概要
 - bluetoothとメッシュネットワークで持ち物の場所を特定することができるデバイス
 - UWBという電場を利用して方角や正確な距離がわかる
   - UWBに対応しているのはiPhone 12以降

## 留意点
 - 正常に動作するには探す対象airtagの近くにapple deviceを持っている人が必要(日本ではあまり心配ない)
 - 一部のデバイスではUWBを対応していなく、大雑把な位置特定になる(数十メートル)

## `手元から離れたときに通知`について
 - `探す`アプリから対象のAirTagの設定に行き、`手元から離れたときに通知`をオンにする
 - 自宅などを例外設定を複数設定することも可能
   - 例えば、ベビーカーならば、"自宅", "保育園"の2つを設定することで離れたとき、音が鳴らなく設定できる

## NFC(Near field communication)タグとしての機能
 - iPhoneやAndroidでNFCタグとして読み取ることができる
   - 読み取った際に[/shortcuts/](/shortcuts/)でイベントを起こすこともできる
 - カードキーで開けるタイプの扉のキーとして設定できる
   - SUICAや白いNFCカードなどを持たなくて済む

## バッテリーの交換
 - `CR2032 3V`の電池で動作する
   - ダイソーなどで販売している
 - airtagsの金属部分を反時計回りに回転するとカバーを外すことができる
   - [AirTag の電池を交換する方法](https://support.apple.com/ja-jp/HT211670)

## ペットや子供につけることの是非
 - 概要
   - 動き回るものや人につけることはAppleとしては非推奨で、子供の見守り目的ならば、インターネット契約があるApple Watchを使用することを薦めている
   - 現実的には、専用のトラッキングデバイスには及ばないものの、ペットや人をトラッキングするデバイスとして十分に機能するとの投稿が多い
     - 所有者から離れると音が出るので、多くの場合、この点が実用に耐えない部分
 - 参考
   - [AirTagを子供に持たせて見守り・位置情報追跡に使えるか試した結果](https://harulog.jp/51842.html)

## 物理的な改造
 - スピーカーを除去する
   - youtube上で様々な人が無音化した例を公開している
 - 参考
   - [How to Remove AirTag Speaker to Mute Apple AirTag](https://www.youtube.com/watch?v=2bozWzHQdVs&ab_channel=MashTips)