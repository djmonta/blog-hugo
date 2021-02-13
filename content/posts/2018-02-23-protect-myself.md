---
layout: post
title: "自分を守る"
date: 2018-02-23 00:27:00 +0900
permalink: /2018/02/23/protect-myself/
---
初めてMongoDBを動かしたのでメモ。

# Start
## run (in background, without authentication)
`$ docker run --name mongodb -v ~/dev/react-tweets/data-dir:/data/db -d mongo:latest`

## exec - mongo shell
`# docker exec -it mongodb mongo admin`

# In Mongo Shell
create a admin user.

```json
db.createUser(
  {
    user: "admin",
    pwd: "password",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
);
```

create a user.

```json
db.createUser(
  {
    user: "react-tweets",
    pwd: "tweetsdb",
    roles: [ { role: "userAdmin", db: "react-tweets" } ]
  }
);
```

----
日記を書かないで寝るよ。何一つ上手くいかない今週だ。仕方ない。  
macOSをアップデートする気持ちになって、HDDフォーマットしてから入れた。まだ入れてないソフト・設定していないこと・消したデータが、次々に出てきそう。  
まぁゆっくりと仕事復帰しようと思ってる
