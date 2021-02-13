---
id: 557
title: Parallels Desktop で Vagrant (Veewee で Box を作成するまで)
date: 2013-12-26 00:00:00 +0900
layout: post
permalink: /2013/12/26/work-vagrant-in-parallels-desktop-create-a-box-in-veewee/
categories:
  - Dev
tags:
  - Vagrant
  - Veewee
---
Mac で ローカルサーバーを立てて、WordPress などのテストをするのは簡単で良いんだけど、最近 <a href="http://www.vagrantup.com/" target="_blank" rel="nofollow external">Vagrant</a> と言うのが流行っているみたいなので取り入れる。
  
<!--more-->

### Vagrant のインストール

まずは、Vagrant を<a href="http://downloads.vagrantup.com/" target="_blank" rel="nofollow external">ダウンロード</a>してインストール。
  
ターミナルで、

<pre class="prettyprint"><code>vagrant -v</code></pre>

として、バージョンが返ってくればOK.

### Vagrant Parallels Provider プラグインのインストール

VirtualBox をデフォルトで使うようだけど、Parallels Desktop を持っているのでそっちを使いたい。
  
<a href="https://github.com/yshahin/vagrant-parallels" target="_blank" rel="nofollow external">Vagrant Parallels Provider</a> というプラグインがあるので使う。

<pre class="prettyprint"><code>vagrant plugin install vagrant-parallels</code></pre>

### Parallels Virtualization SDK 9 for Mac のインストール

<a href="http://www.parallels.com/downloads/desktop/" target="_blank" rel="nofollow external">http://www.parallels.com/downloads/desktop/</a>
  
から Parallels Virtualization SDK をダウンロードしてインストールする。

### Veewee のインストール

<a href="https://github.com/jedi4ever/veewee/blob/master/doc/installation.md" target="_blank" rel="nofollow external">ドキュメント</a>に書かれているとおりやれば良い。

まず、<a href="http://brew.sh" target="_blank" rel="nofollow external">Homebrew</a> で rbenv をインストール。（Homebrew が入ってない場合は、リンク先の一番下の方にインストール方法が書いてある。）

<pre class="prettyprint"><code>brew update
brew install rbenv ruby-build</code></pre>

rbenv の環境設定を書き込んで反映させる。

<pre class="prettyprint"><code>echo 'eval "$(rbenv init -)"' &gt;&gt; ～/.bash_profile
source ～/.bash_profile
</code></pre>

rbenv で veewee をインストールする。

<pre class="prettyprint"><code>rbenv install 1.9.2-p320
rbenv rehash
</code></pre>

Github から veewee をクローン（ホームに veewee フォルダを作成）

<pre class="prettyprint"><code>git clone https://github.com/jedi4ever/veewee.git ～/veewee
cd ～/veewee</code></pre>

Ruby のバージョンを選択する

<pre class="prettyprint"><code>rbenv install 1.9.2-p320
rbenv rehash
rbenv local 1.9.2-p320
</code></pre>

あとは、`bundle install`②をして、自動的に依存関係をクリアしてインストールしてくれる。

<pre class="prettyprint"><code>sudo gem install bundler
sudo bundle install
rbenv rehash
</code></pre>

### テンプレートから定義ファイルの作成

<pre class="prettyprint"><code>bundle exec veewee parallels define 'CentOS-6.4-min' 'CentOS-6.4-i386-minimal'</code></pre>

veewee フォルダの中に definitions/CentOS-6.4-min ができる
  
その中の、&#8221;definitions.rb&#8221; ファイルを編集、
  
ここは変えなくてもいいかもしれないけど、  `:os_type_id => 'RedHat',`
  
を

<pre class="prettyprint"><code>  :os_type_id => 'Centos',</code></pre>

に書き換える。
  
また、もう少し下の方、`"virtualbox.sh"` を

<pre class="prettyprint"><code>     #"virtualbox.sh",
     #"vmfusion.sh",</code></pre>

というようにコメントアウト。で、Box を作成

<pre class="prettyprint"><code>bundle exec veewee parallels build 'CentOS-6.4-min' --workdir=/Users/foo/veewee</code></pre>

（workdirはご自分の環境の合わせて）

最初の方で、ダウンロードする？って聞かれるのでYesと返事。その後ダウンロードなどが自動で行われ、しばらくするとすると Parallels Desktop で インストール開始。
  
再起動したりするが、ターミナルで以下のメッセージが出るまでしばらく待つ。

<pre class="prettyprint"><code>The box CentOS-6.4-min was built successfully!
You can now login to the box with:
ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -p 22 -l veewee 10.211.55.8</code></pre>

最終行をコピペして ssh でログイン。（パスワード veewee / IPアドレスは Parallels の自動割当てで付いたやつなので環境によって違うかも）

### Parallels Tools のインストール

Parallels の 最下部の小さいアイコンの右端の歯車が赤くなってるのをクリックすると、インストール方法など書いたダイアログが出て、「続ける」を押すと Tools の入った iso がマウントされます。

Parallels の画面上でそのまま root でログイン（パスワード vagrant）して

<pre class="prettyprint"><code>mkdir /mnt/dvd
mount /dev/dvd /mnt/dvd
mount -o exec,remount /dev/dvd /mnt/dvd
cd /mnt/dvd
./install</code></pre>

自分の場合、kernel sources がダウンロード出来なかったので、root のまま、

<pre class="prettyprint"><code>yum install kernel</code></pre>

して、リブート後、再度上の作業を行いました。

そして、

<pre class="prettyprint"><code>shutdown -h now</code></pre>

などで、仮想環境を一旦終了。

### Box の Export

<pre class="prettyprint"><code>bundle exec veewee parallels export 'CentOS-6.4-min'</code></pre>

とすれば、veewee フォルダの中に、CentOS-6.40-min.box ファイルが出来ます。

…のはずが、&#8217;Unable to compact the disk&#8217; というエラーが出たので、veewee/lib/veewee/provider/parallels/box/export.rb を編集。
  
&#8211;buildmap オプションが、使えないようで（<a href="https://github.com/yshahin/vagrant-parallels/issues/51" target="_blank" rel="nofollow external">https://github.com/yshahin/vagrant-parallels/issues/51</a>、178行目付近を修正。

<pre class="prettyprint"><code>          # optimize_command = "#{@prldisktool} compact --buildmap --hdd #{path_to_hdd}"
          optimize_command = "#{@prldisktool} compact --hdd #{path_to_hdd}"</code></pre>

これで、Box ファイルが完成。

参考：<a href="http://dkylog.air-nifty.com/dkylog/2013/10/parallelsvagran.html" target="_blank" rel="nofollow external">ParallelsでVagrant &#8211; 自分用Boxを作る: 駄記</a>

続く
