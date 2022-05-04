---
title: Twitch Bot 圖奇機器人(1)
author: Jin Wei
date: 2022-05-04 21:28:00 +0800
categories: [Twith Bot]
tags: [ node.js, twitch bot, javascript]
---

## 需備知識、工具

+ [Visual Studio Code](https://code.visualstudio.com/)
+ node.js
+ Javascript 基本語法

運行環境： MacOs Big Sur 11.6 Mac mini(M1, 2020)

## 環境安裝

Twitch 本身也有機器人建立[教學](https://dev.twitch.tv/docs/irc/get-started)。Twitch 提供一個 IRC 通道，讓機器人可以透過 WebSocket 或 TCP 的方式連到 Twitch，連線後機器人可以在聊天室接收、發送訊息，可以偵測某些特定字說某些話，或者排程說話之類的簡易操作。

1. 首先是 node.js 的安裝，這邊亦有兩種方式。  
    + 確定自己不會在用到 node.js，則可以到 node.js [官方網站](https://nodejs.org/en/)選擇LTS版本安裝。
    + 可能會利用到不同的 node.js 版本則推薦用 nvm 去進行 node.js 的版控，nvm安裝教學[看這邊](https://titangene.github.io/article/nvm.html)  
2. 在安裝好後可用 `node -v` 檢查是否安裝成功，如果安裝成功則會跳出版本號碼，我這邊安裝的是 v14.17.1

```console
    node -v
```

3. 用建立新資料夾，用 VS Code 開啟該資料夾，新增檔案命名為 `bot.js`。在 VS Code 的 Ternimal中輸入 `npm i tmi.js` 安裝 tmi.js 套件（用來連接 Twitch IRC)

```console
    npm i tmi.js
```

4. 接著可以參考 tmi.js 所提供的[範例程式碼](https://tmijs.com/#getting-started)，將他複製貼上到剛新增的 `bot.js` 裡頭，程式碼如下所示。

```

const tmi = require('tmi.js');

const client = new tmi.Client({
 options: { debug: true },
 identity: {
    username: 'my_bot_name',
    password: 'oauth:my_bot_token'
 },
 channels: [ 'my_name' ]
});

client.connect();

client.on('message', (channel, tags, message, self) => {
 // Ignore echoed messages.
 if(self) return;

 if(message.toLowerCase() === '!hello') {
  // "@alca, heya!"
  client.say(channel, `@${tags.username}, heya!`);
 }
});

```

5. 其中有三個地方的值需要進行修改

+ username : `my_bot_name` 請修改成你要用的機器人帳號的英文ID，假設帳號為 `卡北齊(shawno439)` 那我其中該輸入的就為 `shawno439`
+ password: `oauth:my_bot_token` 可利用這個 [網站](https://twitchapps.com/tmi/) 取得你的 Twitch Oauth，將其複製貼上，OAUTH格式應該為 `oauth:XXXXXXXXXXXXXX`
+ channels: [ `my_name` ] 這邊則是填入要加入的聊天室名稱，要注意有些聊天室有需要追蹤一定時間才可說話的規定。（建議在第一次執行或是測試功能時皆在自己的Twitch頻道，比較不會打擾到人也不會遇到擋重複留言的問題呦！）

6. 當以上都調整完時，在 Ternimal 輸入 `node bot.js` 執行程式碼。

```console
    node bot.js
```

7. 最終顯示 `[22:18] info: Joined #XXXXXX` 代表機器人已經成功加入該聊天室了。這時候可以到設定的 Twitch聊天室輸入 `!hello`，機器人會回答 `heya!`  

最終建立Twitch的第一步就完成了，後續會再分享一些可能會用到的 JavaScript 語法以及連接 Twitch API 的方法。

