---
layout: post
title: "google apps script"
date: 2021-06-01
excerpt: "google apps scriptの使い方"
project: false
config: true
tag: ["google apps script", "spreadsheets"]
comments: false
---

# google apps scriptの使い方
 - [google spreadsheets](/google-spreadsheets/)等で使用できるJavaScriptのスクリプト

## google spreadsheetsでの関数の作り方
 - `[拡張機能]` -> `[Apps Script]`

 1. 関数をイベントに紐付けるイメージ(C#に近い)
 2. ローカルで実行するには`[保存]` -> `[実行]`

### チートシート

#### spreadsheet上のオブジェクトに関数を紐付ける
 - `画像等を貼り付ける` -> `画像のハンバーガーボタンを押して[スクリプトを割り当て]を選択` -> `関数名を入力する`  
   - オブジェクトに関数を割り当てると、左クリックか、二本指クリックでしかオブジェクトを操作できなくなる

#### ログ
 - `Logger.log`
   - IDEで表示される
 - `Browser.msgBox`
   - gssでメッセージボックスで表示される

#### タイマーを用いて処理をバッチ化する
 - `App Scriptの画面から[トリガー]を選択` -> `[トリガーを追加]を選択` -> `[時間主導型]を選択` -> `好きな時間粒度で選択`

#### sheetのIDを取得

```js
var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
sheet.getSheetId();
```

#### sheetの名前を取得

```js
var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
sheet.getName();
```

#### 操作しているユーザの取得

```js
Session.getEffectiveUser().getEmail();
```

#### 画像のダウンロードと挿入

```js
var image = "http://img.labnol.org/logo.png";
var blob = UrlFetchApp.fetch(image).getBlob();
var ss = SpreadsheetApp.getActiveSpreadsheet();
var sheet = ss.getActiveSheet();
sheet.insertImage(blob, 4, 3);
```

#### セルの情報を読み込み

```js
var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
var values = sheet.getSheetValues(1,1,100, 3); // レンジで読み取っているのでアクセスするにはvalues[x][y]のようにする
Logger.log(JSON.stringify(values));
```

#### シートにかかれているすべての情報を読み込み、必要なカラムだけ抽出する

```js
var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
var lastRow = sheet.getLastRow();
var lastColumn = sheet.getLastColumn();

var values = sheet.getSheetValues(1,1,lastRow,lastColumn);
cols = values[0];
// id, title, contentをパース
obj = {"id": [], "title":[], "content": []};
for (let col_idx = 0; col_idx < cols.length; col_idx++) {
  if(cols[col_idx] == "id" || cols[col_idx] == "title" || cols[col_idx] == "content") {
    col_name = cols[col_idx];
    for(let row_idx = 1; row_idx < values.length; row_idx++) {
      obj[col_name].push(values[row_idx][col_idx]);
    }
  } 
}
```
 - `sheet.getLastColumn()`, `sheet.getLastRow()`でデータが入っている最大の範囲を取得できる
 - `obj`で必要なカラムのデータだけを取得する


#### 特定のURLにpostデータを付けてアクセスする

```js
var data = {
  'name': 'Bob Smith',
  'age': 35,
  'pets': ['fido', 'fluffy']
};
var options = {
  'method' : 'post',
  'contentType': 'application/json',
  // Convert the JavaScript object to a JSON string.
  'payload' : JSON.stringify(data)
};
var response = UrlFetchApp.fetch("http://6c3a8d888880.ngrok.io", options);
Logger.log(response.getContentText());
```

#### APIで取得したjson情報をパースしてシートに貼り付け

```js
var response = UrlFetchApp.fetch("http://6c3a8d888880.ngrok.io", options);
var data = JSON.parse(response.getContentText());
sheet.getRange(2, 1, data.length, data[0].length).setValues(data);
```

#### セルを指定して最後のセルにデータを貼り付け

```js
append_cols = ["score1", "score2", "score3"];

for (const [index, append_col] of append_cols.entries()) {
  const last_col_idx = sheet.getLastColumn();
  sheet.getRange(1, last_col_idx + 1).setValue(append_col);
  for(let row_idx = 1; row_idx < values.length; row_idx++) {
    sheet.getRange(1 + row_idx, last_col_idx + 1).setValue("VALUE");
  }
}
```
 - 範囲指定しない挿入は遅い

#### localhostへのAPIへアクセスしたい
 - ngrokを使う  

```js
var response = UrlFetchApp.fetch("http://*****.ngrok.io");
Logger.log(response.getContentText());
```

#### トーストの表示

```js
// トーストの開始
SpreadsheetApp.getActiveSpreadsheet().toast("なにか処理しています...",-1);
// トーストの終了
SpreadsheetApp.getActiveSpreadsheet().toast("完了.");
```

---

## 例; コンピュートエンジンの自動停止

```js
var token = ScriptApp.getOAuthToken();
var options = {
  'method' : 'post',
  'contentType': 'application/json',
  headers: {'Authorization': 'Bearer ' + token}
};
STOP_INSTANCES_URL = "https://www.googleapis.com/compute/v1/projects/%s/zones/%s/instances/%s/stop";
var target = Utilities.formatString(STOP_INSTANCES_URL, "starry-lattice-256603", "asia-northeast1-b", "my-vm");
var results = UrlFetchApp.fetch(target, options);
Logger.log(results);
```

--- 

## 参考になったページ
 - [GASでCompute Engineの時間に応じた自動停止/起動ツールを作成する 〜GASで簡単に好きなGoogle APIを叩く方法〜](https://www.kabuku.co.jp/developers/gcs-auto-scheduler-by-gas)