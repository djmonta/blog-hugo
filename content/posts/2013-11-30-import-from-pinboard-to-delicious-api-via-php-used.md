---
id: 555
title: Pinboard から Delicious へインポート (API経由 PHP 使用)
date: 2013-11-30 00:00:00 +0900
layout: post
permalink: /2013/11/30/import-from-pinboard-to-delicious-api-via-php-used/
categories:
  - Dev
tags:
  - del.cio.us
  - PHP
  - pinboard
---
[delicious](http://delicious.com/) が消えるって話があったよね、その時に、[Pinboard](http://pinboard.in) に乗り換えたんだけど、結局消えずに残ってるから、一応データを同期させるために、いろいろやった。
  
Pinboard からエキスポートできるファイルは、XML, HTML, JSON とあるんだけど、delicious は HTML しかインポートできなくって、なぜか HTML だと文字化けしてしまうので、頑張って PHP 書いた。変なところがあったら教えて下さい。

<!--more-->

<pre class="prettyprint linenums"><code language="php"><?php
$dusername = "USERNAME";
$dpassword = "PASSWORD";

if (file_exists('delicious-toimport.xml')) {
  $xml = simplexml_load_file('delicious-toimport.xml');
} else {
  exit('Failed to open delicious-toimport.xml.');
}

for($i=0; $i<count($xml->post); $i++){
  $post = $xml->post[$i];
  $link = urlencode((string)$post['href']);
  $desc = urlencode((string)$post['description']);
  $ext = urlencode((string)$post['extended']);
  $tag = (string)$post['tag'];
  $tags = urlencode(str_replace(" ", ",", $tag));
  $date = urlencode((string)$post['time']);
  // var_dump($tags);

  $api = 'api.del.icio.us/v1';  
  $apicall = "https://$dusername:$dpassword@$api/posts/add?&url=$link&description=$desc&extended=$ext&tags=$tags&dt=$date";
  $ch = curl_init($apicall);  
  curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 2);  
  curl_setopt($ch, CURLOPT_USERAGENT, 'php - curl');  
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);  
  curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
  $response = curl_exec($ch);   

  curl_close($ch);
  var_dump($response);
}
?></code>
</pre>

んーこれ書くのに1時間ぐらいかかったけど、もっとささっと書けるようになりたいものですね。
  
今後は、[IFTTT](http://ifttt.com/) を使って、同期しようと思ってます。
