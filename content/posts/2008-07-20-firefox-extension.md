---
id: 457
title: Firefoxの拡張を書き出してみる
date: 2008-07-20 00:00:00 +0900
layout: post
permalink: /2008/07/20/firefox-extension/
categories:
  - Items
tags:
  - Firefox
---
Firefox 3 になってから、しばらく経って拡張等落ち着いてきたのでここにメモ代わりにまとめ。
  
標準の Firefox だと、[ustream.tv](http://ustream.tv) のチャットやら、Google Talk Gadget 等のFlashのテキストフィールドに日本語が入力できない問題 [(Bug 357670)](https://bugzilla.mozilla.org/show_bug.cgi?id=357670) があるので、パッチを当ててある、Firefox lzyc ビルドを使ってます。

<!--more-->

[AutoCopy](http://autocopy.mozdev.org/) 0.8 
:   :選択文字列を自動的にコピー。そのままコンテキストメニューが出てロケーションバーや検索バーに貼付けたりもできる。これ便利。手放せない。

[1Password](http://www.1passwd.com/) 2.7.2 
:   :ID/パスワード自動入力

[All-in-One Sidebar](http://firefox.exxile.net/aios/) 0.7.6 
:   :サイドバー拡張。自動で閉じる設定が便利

[ColorZilla](http://www.colorzilla.com/) 2.0 
:   :色スポイトツール。設定した形式で自動でクリップボードにコピー。

[del.icio.us Complete](http://delicious.mozdev.org/) 1.3 [disabled]
:   :Firefox 3 未対応のため使えないけど、Delicious Bookmarks よりこっちを使ってたのはなんでだっけか忘れた。

[del.icio.us IncSearch](http://www.enjoyxstudy.com/firefox/extension/delicious_incsearch/) 1.10.4 
:   :[del.icio.us](http://del.icio.us/) をインクリメンタルサーチできる

[Delicious Bookmarks](http://delicious.com) 2.0.72 
:   :[del.icio.us](http://del.icio.us/) にポストするときはこれ。あとサイドバーでタグからたブックマークを探したり。Firefox のブックマークを置き換える機能は使ってない

[DOM Inspector](http://www.mozilla.org/projects/inspector/) 2.0.0 
:   :Firefox のウィンドウの属性等を知れる。見た目を CSS でいじる時のために。

[DownloadHelper](http://www.downloadhelper.net) 3.1.1 
:   :[YouTube](http://youtube.com) 等動画サイトのファイルをダウンロード。なんだかんだでこれでダウンロードして手動で変換作業することが多い

[DownThemAll!](http://downthemall.net/) 1.0.3 
:   :ダウンローダ。画像を一気にダウンロードする時とか便利。

dragdropupload 1.6.7 
:   :アップロードする際にファイルをドラッグアンドドロップで選択できる

[FaviconizeTab](http://espion.just-size.jp/archives/06/308085916.html) 0.9.8.2 
:   :タブをファビコンだけの表示にする

[FEBE](http://customsoftwareconsult.com/extensions) 6.0b(20080612_085122) 
:   :拡張/プロファイルバックアップ

[Google Toolbar for Firefox](http://www.google.com/) 3.1.20080605M 
:   :英単語のマウスオーバーで訳をツールチップ表示のためだけに入れてる

[Greasemonkey](http://www.greasespot.net/) 0.8.20080609.0 
:   :いろんなスクリプト入れてます。数えたら32個。[Tumblr](http://www.tumblr.com) / [Google Reader](http://reader.google.com) 関連多し。

[InfoLister](http://mozilla.doslash.org/infolister) 0.10 
:   :拡張リスト出力

[Make Link](http://www.soylentred.net/projects/make-link) 8.07 
:   :URL/タイトル/選択文字列を、右クリックから形式を指定してクリップボードにコピー

[Nightly Tester Tools](http://www.oxymoronical.com/web/firefox/nightly) 2.0.2 
:   :古い拡張を使うために入れてる

[OpenSearchFox]() 0.1.5 
:   :検索バープラグインを作る。

[PicLens](http://www.piclens.com/) 1.7.0.3459 
:   :[Flickr](http://flickr.com) / [Googleイメージ検索結果](http://images.google.com) などの画像をフルスクリーンでスムーズにたくさん表示。でも、見てると酔うのであまり使わない

[Quartz PDF Plugin](http://code.google.com/p/firefox-mac-pdf) 0.9.8 
:   :Firefox 内で PDF を表示させる

[RefControl](http://www.stardrifter.org/refcontrol/) 0.8.11 
:   :Referer を偽装したり。[Tumblr](http://www.tumblr.com) のために使ってる

Smart Bookmarks Bar 1.4.1 
:   :ブックマークバーのブックマークをファビコン表示、マウスオーバー時のみタイトル表示。

[Stylish](http://userstyles.org/stylish/) 0.5.7 
:   :いろんなサイトや Firefox 自体の見た目を CSS で変える。数えたら12個。思ったより少ないけど、Google関連は必須。

[Tab Mix Plus](http://tmp.garyr.net) 0.3.6.1.080416 
:   :タブ関連の設定を拡張。基本的には新規タブで開く設定

[TiddlySnip](http://tiddlysnip.com) 1.0 RC1 
:   :ローカルの1ファイルで動く Wiki、[TiddlyWiki](http://www.tiddlywiki.com/) に右クリックからメモるための拡張

[Tombloo](http://code.google.com/p/tombloo/) 0.3.8.2 
:   :[Tumblr](http://www.tumblr.com) のみならず、いろんなサービスに右クリックからポストできる超便利な拡張。個人的には Tumblr バックアップ機能がはずせない。

TwitterFox 1.6 
:   :Firefox でも [Twitter](http://twitter.com)。でも、基本は夏ライオンというクライアントソフトで見てます。

[Undo Closed Tabs Button](http://code.google.com/p/uctb/) 3.0.3 
:   :閉じたタブを再び開くツールバーアイコン。

[Web Developer [日本語版]](http://chrispederick.com/work/web-developer/) 1.1.6 
:   :サイト作る際に便利なツールバー

以上の30個（うち1個は無効中）の拡張を使ってました。Mac には、Safari というすばらしいブラウザがあるんだけど（文字の描写はピカイチすごく綺麗）、ここまで自分用にカスタマイズしてあると離れられなくて、Windows でも同じように使えるしで、Firefox がデフォルトブラウザです。
  
テーマは [GrApple Delicious (blue)](http://www.takebacktheweb.org/) を使ってます。Mac Firefox 標準のでも別に良かったけどアイコンがなんとなく気に入らなかったので。
  
書いていて気がついたのは、自動系はほんと便利。あと、右クリックメニューが汚いので直したいとか。
