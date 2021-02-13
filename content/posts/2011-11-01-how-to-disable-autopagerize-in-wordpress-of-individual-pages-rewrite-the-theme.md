---
id: 524
title: WordPress の個別ページで AutoPagerize を無効にする方法（テーマを書き換える）
date: 2011-11-01 00:00:00 +0900
layout: post
permalink: /2011/11/01/how-to-disable-autopagerize-in-wordpress-of-individual-pages-rewrite-the-theme/
categories:
  - Blog
tags:
  - Wordpress
---
<a href="http://autopagerize.net" rel="external nofollow">AutoPagerize</a> を入れていると、次のページをどんどん継ぎ足していってくれて、これなしにはWebブラウジングしたくないくらいくらい便利なのです。
  
ところが、Wordpress のブログで、個別ページのときはコメントが流れてしまったりするので、機能させたくないんです。
  
<!--more-->

調べてみると、Microformat の hentry というクラスに AutoPagerize が反応しているらしい。
  
そこで、個別ページでは hentry クラスを除くフィルターを作りました。

テーマの functions.php に、

<pre class="prettyprint linenums">&lt;codee language="php">function remove_hentry( $classes ) {

    $classes = array_diff($classes, array('hentry'));
    return $classes;
}
&lt;/code>
</pre>

と書いて、single.php (page.php も可) の最初に、

<pre class="prettyprint linenums">&lt;codee language="php">add_filter('post_class', 'remove_hentry');&lt;/code>
</pre>

と書けば、hentry クラスが 除かれ、AutoPagerize は無効になるはずです。

これは、Wordpress でブログを作っているあらゆる方にオススメしたい。コメントや広告、流れちゃって見づらくなっちゃってます。
  
それか、Microformat をいじるのも何だかいまいちな気がするので AutoPagerize 側でどうにか対処していただくとありがたいのだけど。
