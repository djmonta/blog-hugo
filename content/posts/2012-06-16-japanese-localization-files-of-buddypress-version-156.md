---
id: 531
title: BuddyPress の日本語化ファイル Version 1.5.6
date: 2012-06-16 00:00:00 +0900
layout: post
permalink: /2012/06/16/japanese-localization-files-of-buddypress-version-156/
categories:
  - Blog
tags:
  - BuddyPress
  - Wordpress
  - 日本語化
---
BuddyPress の日本語化はいろんなところで行われているようだけど、どこで最新のファイルが手に入るのかよく分からなかったので、自分で作りました。
  
~~buddypress-ja_1.5.6.zip~~

<!--more-->

ダウンロード・解凍して、wp-content/plugins/buddypress/bp-languages に、buddypress-ja.mo ファイルをアップロードすれば完成です。
  
一部、変な翻訳の箇所がありますが、大体使えると思います。気になる場合は、buddypress-ja.po ファイルを編集してください。

Mo ファイルを作るには、gettext を入れて以下のコマンド、または PoEdit 等で作ります。詳しくは「po mo 変換」とかで検索してください。
  
`msgfmt -o /path/to/file.mo /path/to/file.po`
