---
id: 578
title: '[解決済み] El Capitan のシステム環境設定から iCloud にログイン出来ない。'
date: 2015-10-23 00:00:00 +0900
layout: post
permalink: /2015/10/23/resolved-can-not-log-in-to-the-icloud-system-preferences-of-el-capitan/
categories:
  - Diary
tags:
  - Mac OS
---

El Capitan をクリーンインストールしたのですが、表題の通り、システム環境設定の iCloud からログインしようとすると、「&#8221;(メールアドレス)&#8221; に問題があるため、このMacをiCloudに接続できません。」と出てきちゃう。
  
<!--more-->

<img src="media/20151024_022021_1.png" alt="20151024_022021_1" class="alignnone size-full wp-image-3299" />

始めは、iCloudキーチェーンの問題で、セキュリティコードのあとの確認SMSが届かないこと、だったのだけど。
  
Apple のサポートに電話して、本人確認の後、SMSは回避して使えるようにしてもらい、いろいろ試してるうちに、ログインできない問題に発展。
  
1時間半ぐらい電話で話して、試したのは、他のアプリケーションでログイン出来るかどうか（App Store, iTunes, FaceTime, Message あたり）。これは問題なく、使えてる。
  
あとテストアカウントを作って同じiCloudアカウントでログイン出来るか。これはログイン出来ない状態。
  
最後に、`/Library/Preferences/SystemConfiguration/com.apple.airport.preferences.plist` と、同じフォルダ内の

    com.apple.captive.probe.plist
    com.apple.smb.server.plist
    com.apple.wifi.message-tracer.plist
    NetworkInterfaces.plist
    preferences.plist
    

の 6ファイルを削除後、再起動をかけたら、ログイン出来たっぽい感じで電話を切ってしまったんだけど、10秒ぐらいするとまた同じエラーメッセージが出てきて、もう。。。
  
パスワードを入れた後「不明なエラー」が出ることもあったりと、なかなかの謎っぷり。

英語でも検索してみて、試したことは、`～/Library/Application Support/iCloud/Accounts` の中身を消すとか、
  
`～/Library/Preferences/MobileMeAccounts.plist` を削除するとか、
  
キーチェーンアクセスで、ログインキーチェーンの中にある、分類がパスワードの、名前がiCloudのメールアドレスの項目（種類はアプリケーションパスワード）を開いて、「パスワードを表示」にチェックを入れたあと、表示されるランダムな英数字のパスワードを消して、iCloudのパスワードを入れて、保存してみる、とか。

全部ダメで、結局まだ解決しておりません。

iPhone も復元したあとだったので、iCloudキーチェーンをONにしてなかったことに気づき、他のデバイスからの承認が出来なかったんだけど、なんかいろいろやってるうちに、SMSが届いたりして、iPhone の方は、ばっちりログイン出来ている状況。Mac が、Mac mini も、MacBook Air も同じタイミングでクリーンインストールしたし、同じ感じでログイン出来ない。
  
iCloud Drive は同期できてる様子だし、連絡先やらカレンダーも使えてるから、特に大きな問題はなさそうだから、良いんだけど、、、バグですかね。

<ins datetime="2015-10-24T09:24:34+00:00">追記 2015/10/24 18:25 解決しました！</ins>
  
昨日の夕方はやってもダメだったのに、今日になって、サインアウト->再起動かけたら、普通に何のアラートも出ず、大丈夫になりました。
  
何かサーバー側で対応していただいたのか、分かりませんが、とにかく、解決した。
  
おかしかったのがウソのようで腹が立つけど、まあ良いや。
