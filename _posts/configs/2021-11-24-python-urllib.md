---
layout: post
title: "urllib"
date: "2021-11-24"
excerpt: "urllibモジュールの使い方"
project: false
config: true
tag: ["urllib", "python"]
comments: false
sort_key: "2022-05-20"
update_dates: ["2022-05-20"]
---

# urllibモジュールの使い方

## 概要
 - python3のURLハンドリングモジュール
 - urlのパラメータの組み立て、パース
 - urlからのデータ取得を行える

## 具体例例

### urlを要素ごとに分ける

```python
from urllib import poarse
x = parse.urlparse("https://news.yahoo.co.jp/something?a=b")
display(x)
# ParseResult(scheme='https', netloc='news.yahoo.co.jp', path='/something', params='', query='a=b', fragment='')
```

### パースした一部の要素を変更する

```python
x = parse.urlparse("https://news.yahoo.co.jp/something?a=b")
x._replace(scheme="http")
display(x)
# ParseResult(scheme='http', netloc='news.yahoo.co.jp', path='/something', params='', query='a=b', fragment='')
```

### パースしたオブジェクトからstr型のURLを得る

```python
x = urlparse("https://news.yahoo.co.jp/something?a=b")
x._replace(scheme="http")
display(x.geturl())
# 'https://news.yahoo.co.jp/something?a=b'
```

### 相対パスから絶対パスを得る

```python
parse.urljoin("https://news.yahoo.co.jp/ex0/ex1/?a=b", "../../relative.html")
# 'https://news.yahoo.co.jp/relative.html'
```

### URLパラメータ(クエリ)のパース

```python
# URLパラメータ(クエリ)のパース
from urllib import parse
display(parse.parse_qs("key1=1&key2=2")) # {'key1': ['1'], 'key2': ['2']}
```

### URLパラメータ(クエリ)の組み立て

```python
from urllib import parse
parse.urlencode({"key1": 1, "key2": 2, "japanese": "日本語"}) # key1=1&key2=2&japanese=%E6%97%A5%E6%9C%AC%E8%AA%9E
```

### URLからデータを取得

```python
from urllib import request
with request.urlopen("http://example.com") as fp:
    print(fp.read().decode())
"""
<!doctype html>
<html>
<head>
    <title>Example Domain</title>
...
"""
```

## Google Colab
 - [python-urllib](https://colab.research.google.com/drive/1l4aUlJXthmDewMSVSRwFlnuW0_wJnsf_?usp=sharing)
