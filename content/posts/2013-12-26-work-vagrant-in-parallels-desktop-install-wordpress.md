---
id: 558
title: Parallels Desktop で Vagrant (WordPress インストールまで)
date: 2013-12-26 00:00:00 +0900
layout: post
permalink: /2013/12/26/work-vagrant-in-parallels-desktop-install-wordpress/
categories:
  - Dev
tags:
  - Vagrant
  - Wordpress
---
[前回](http://monta.ampomtan.com/2579)の続き。

WordPress の開発に使えたら便利ですよね。というわけで、VCCW(Vagrant-Chef-Centos-Wordpress) を使ってみます。

<!--more-->

### Vagrant に Box を追加

<pre class="prettyprint"><code>vagrant box add CentOS-6.4-min ～/veewee/CentOS-6.4-min.box --provider=parallels</code></pre>

### VCCW の設定

vagrant-hostsupdater をインストール。

<pre class="prettyprint"><code>vagrant plugin install vagrant-hostsupdater</code></pre>

WordPress を使いたいフォルダで、Vagrantファイルをクローン。

<pre class="prettyprint"><code>git clone https://github.com/miya0001/vagrant-chef-centos-wordpress.git vagrant-wp</code></pre>

<pre class="prettyprint"><code>cd vagrant-wp
cp Vagrantfile.sample Vagrantfile</code></pre>

### site-cookbook（レシピ）の書き換え

そのままだと、apache が入らないとエラーが出ます。(Error executing action `install` on resource &#8216;package[apache2]&#8217;)
  
これは、Vagrantfile の52行目をコメントアウトすることで回避。

<pre class="prettyprint"><code>  #config.vm.synced_folder "www/", "/var/www", :create => true</code></pre>

また、Create /var/www/wordpress Permission Denied のエラーは、site-cookbook/wp-install/recipes/default.rb の編集。55行目あたりに、挿入。

<pre class="prettyprint"><code>bash "chown /var/www" do
  user "root"
  group "root"
  code "chown -R vagrant:vagrant /var/www"
end</code></pre>

### Vagrantfile の編集

11行目。

<pre class="prettyprint"><code>WP_LANG              = "ja" # WordPress locale (e.g. ja)</code></pre>

46行目。

<pre class="prettyprint"><code>  config.vm.box = "CentOS-6.4-min"
  # config.vm.box_url = "http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-i386-v20130427.box"</code></pre>

### Vagrant up

やっと、、、

<pre class="prettyprint"><code>vagrant up --provider=parallels</code></pre>

### NIC のエラー

Box をコピーしたので、「Device eth0 does not seem to be present, delaying initialization」などのエラーが出ると思います。
  
これは、`vagrant ssh` して、バーチャルマシンに入り、
  
`ifconfig -a` を実行して eth0 が存在しない事を確認する
  
/etc/udev/rules.d/70-persistent-net.rules ファイルを編集し、NAME=&#8221;eth0&#8243; と記述されてる行を削除し、
  
NAME=&#8221;eth1&#8243; と記述されている箇所を NAME=&#8221;eth0&#8243; に書き換えサーバーを再起動します。

### 共有フォルダの設定

このままでは、Mac 側から SSH でないとファイルがいじれないので、共有フォルダを設定します。
  
Vagrantfile の、先ほどコメントアウトした52行目を使います。

<pre class="prettyprint"><code>  config.vm.synced_folder "www/", "/var/www",
    owner: "vagrant", group: "vagrant"</code></pre>

と書き換え、Mac 側に www フォルダを作っておきます。

反映させるには、`vagrant reload` です。

ここでもう一度、`vagrant provision` しなければなりません。
  
Mac 側のブラウザから、wordpress.local にアクセスしてみると、Wordpress がインストールされています。
  
また、www/wordpress フォルダをいじれば、そのままバーチャルマシンの /var/www/wordpress をいじることになります。
  
以上になります。

最後の方、なんだか冗長なことをしているので、詳しい人！解決策を教えて下さいませー！！

参考：<a href="http://www.linuxmaster.jp/linux_blog/2011/09/vmwaredevice-eth0-does-not-seem-to-be-present-delaying-initialization.html" target="_blank" rel="nofollow external">VMwareで「Device eth0 does not seem to be present, delaying initialization」と表示された時の対処法　その２｜リナックスマスター.JP 公式ブログ</a>
