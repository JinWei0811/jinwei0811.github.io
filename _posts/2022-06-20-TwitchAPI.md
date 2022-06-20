---
title: Twitch Bot圖奇機器人(3)-查詢Twitch API
author: Jin Wei
date: 2022-06-20 23:05:00 +0800
categories: [Twitch Bot, Twitch API]
tags: [node.js, twitch api, fetch]
---

## 須備知識、工具

+ [Visual Studio Code](https://code.visualstudio.com/)
+ Javascript語法（fetch, json）
+ 已搭建完成機器人執行環境[可參考](https://jinwei0811.github.io/posts/TwitchBot/)

## Twitch API 介紹

Twitch Api是 twitch所提供的服務，可以做一些簡單的查詢，在這個[網頁](https://dev.twitch.tv/docs/api/reference)中有提供所有可利用Twitch API做到的功能。  
Twitch API是RESTful API的形式，在這篇文章中會用到`fetch`的方式去呼叫，然後再轉成 `Json` 的格式去取得我們想取得的值。  
其中我認為比較有用的功能

1. Get Users 取得使用者[資訊](https://dev.twitch.tv/docs/api/reference#get-users)
2. Get Followed Streams 取得使用者追隨頻道[資訊](https://dev.twitch.tv/docs/api/reference#get-followed-streams)
3. Get Users Follows 取得使用者追隨特定頻道[資訊](https://dev.twitch.tv/docs/api/reference#get-users-follows)

## 取得 Twitch 金鑰

發Twitch API需要先獲得憑證（OUATH)  

1. Client-ID
2. Authorization  

這邊提供一個別人所提供的[服務](https://twitchtokengenerator.com/)來取得Twitch憑證

1. 進去之後先選擇為 Bot Chat Token
2. 給予Twitch授權
3. 往下滑有個表格標頭為 `Generated Tokens`  

其中 ACCESS TOKEN 就是你的 `Authorization` , CLIENT ID就是你的 `Client-ID` ，把這兩串文字記好待會會用到。

## 呼叫Twitch API

既然已經取得 `Authorization` 、 `Client-ID` 就可以來嘗試呼叫Twitch API。（以下皆用Get Users當作範例）  

1. 首先設定一個Heade參數，放入剛才取得的授權憑證。將 `<your Authorization>` 替換成你的 `Authorization`，Client-ID同理。

```
let headers = {
  Authorization: 'Bearer <your Authorization>',
  Client-Id: '<your Client-ID>',
};
```

2. 呼叫Twitch API，user_name 就是你要查詢的使用者的 Twitch 英文ID。假設我Twitch顯示的名稱是 `浣熊機器人 (raccattack_bot)` 那麼要輸入的user_name 應該是 `raccattack_bot`。  
這串程式碼主要意思是，利用GET的方式並且放入headrs來呼叫Twitch API，將從Twitch取回來的資料轉成Json格式，再將它印出來。

```
fetch(`https://api.twitch.tv/helix/users?login=${user_name}`, {
    method: "GET",
    headers: headers,
    })
    .then((response) => response.json())
    .then((result) => { console.log(result) });
```

以 浣熊機器人(raccattack_bot) 為例，當我在 user_name 填入 `raccattack_bot`，從Twitch取回來的資料(result)如下：  
這就是一個標準的Json格式，假設我要 `id` 這項的值，只需要呼叫 `result.data[0].id` 就可取得。  
基本上到這邊應該都可以做到Twitch API的呼叫了，呼叫API只是第一步，將取得回來的JSON檔加工成我們要的內容在輸出，這部分就依自己的需求去做呈現，就不多加贅述了。

```
{
  data: [
    {
      id: '87572734',
      login: 'raccattack_bot',
      display_name: '浣熊機器人',
      type: '',
      broadcaster_type: '',
      description: '',
      profile_image_url: 'https://static-cdn.jtvnw.net/user-default-pictures-uv/294c98b5-e34d-42cd-a8f0-140b72fba9b0-profile_image-300x300.png',
      offline_image_url: '',
      view_count: 166,
      created_at: '2015-04-05T09:23:57Z'
    }
  ]
}
```
  
如果有遇到任何的問題歡迎在下面留言，或者寄信給我交流討論～