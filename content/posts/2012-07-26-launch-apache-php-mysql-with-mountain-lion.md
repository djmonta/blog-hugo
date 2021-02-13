---
id: 534
title: Mountain Lion で Apache、PHP、MySQLを動かす
date: 2012-07-26 00:00:00 +0900
layout: post
permalink: /2012/07/26/launch-apache-php-mysql-with-mountain-lion/
categories:
  - Dev
tags:
  - Mac OS
---
Mountain Lion を入れたら、システム環境設定から、Web 共有が消えてました。Apache は入ってるので、設定方法。
  
<!--more-->

### Apache

ターミナルで、

<pre class="prettyprint"><code> $ sudo apachectl start</code>
</pre>

http://localhost/ にアクセスすると、/Library/WebServer/Documents 以下のファイルが表示されます。
  
この設定を変えたい場合は、/etc/apache2/users/ユーザー名.conf というファイルを作成し、以下のような記述で保存します。

<pre class="prettyprint"><code>DocumentRoot "/path/to/documentroot"</code>
</pre>

再度ターミナルで

<pre class="prettyprint"><code> $ sudo apachectl restart</code>
</pre>

とすれば、設定が反映されます。

### PHP

/etc/apache2/httpd.conf を編集して、PHP を有効にします。

<pre class="prettyprint"><code>#LoadModule php5_module libexec/apache2/libphp5.so</code>
</pre>

の行を検索して、先頭の#を取り除いてあげればOK. Apache を再起動すると動きます。

### MySQL

Homebrew で MySQL をインストールしていたものが動いている前提です。
  
/etc/php.ini.default をコピーして、php.ini を作成。

<pre class="prettyprint"><code>mysql.default_socket = /tmp/mysql.sock</code>
</pre>

にしてあげれば、動くはずです。

メモ書きのような感じになってしまいましたが、お役に立てれば幸いです。
