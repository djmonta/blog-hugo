---
id: 458
title: アマゾンのプラグイン
date: 2008-07-21 00:00:00 +0900
layout: post
permalink: /2008/07/21/amazon-plug-in/
categories:
  - Blog
tags:
  - amazon
  - Wordpress
---
[wp-tmkm-amazonプラグイン配布](http://blog.openmedialabo.net/wordpress/wp-tmkm-amazon)

これだー。素晴らしい。Wordpress の Amazon プラグイン。
  
エントリー内に `[tmkm-amazon]ASIN番号[/tmkm-amazon]`と書けば、Amazon Web Service 経由で情報を引っ張ってきて表示できる。今まで自分の用意した XSL から HTML ソースをコピーしてってやってたやつ全部置き換えた。
  
導入もわりかし簡単だったし、とても便利。

ついでに、Amazon のページを開いてるときにASINをコピーできるような bookmarklet をつくった。

<pre class="prettyprint"><code language="javascript">javascript:var%20li=document.getElementsByTagName('li'),i=0,e,t;while(e=li%5Bi++%5D)void((t=e.innerHTML).match(/ASIN:%7CISBN-10:/)&&prompt('ASIN/ISBN-10',t.replace(/%5E.+%20(.+)$/,'$1')))</code>
</pre>

まとめてリスト表示もできるみたいだから後で試す。
