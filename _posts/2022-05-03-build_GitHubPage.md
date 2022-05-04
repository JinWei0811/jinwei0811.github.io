---
title: 搭建 GitHubPage
author: Jin Wei
date: 2022-05-03 20:49:00 +0800
categories: [GitHub Page]
tags: [Github Page, Jekyll, Chirpy]
---

## 必備知識
1. Github操作
2. CMD基本操作
3. MarkDown基本操作

系統環境為 `Windows11 21H2`（環境僅供參考，如同為Windows系統，操作應該大同小異）

## Github Page , Jekyll

我所選用的模板是 [Chirpy Jekyll Theme](https://github.com/cotes2020/jekyll-theme-chirpy)，在其 Github 下面有詳細的操作流程，但這邊還是分享自己的流程以供參考。  
因為搭建 Github Page 是基於 Jekyll，所以要先至[Jkeyll.com](https://jekyllrb.com/docs/installation/)參考環境安裝流程。  

1. 安裝Ruby，最方便快捷的是到[RubyInstaller for Windows](https://rubyinstaller.org/)  
    + 需安裝 RubyInstaller-2.4 以上的版本
    1. 下載並安裝 Ruby + Devkit(默認安裝就可以，無腦NEXT XD)
    2. 開啟 CMD 輸入 ruby -v ，檢查是否正確安裝 Ruby，這邊我安裝的版本是 Ruby 3.1.2p20  

    ```console
      $ ruby -v
    ```

    3. 在 CMD 輸入 ridk install，一樣選擇 base 版本(1 - MSYS2 base installation)即可  

    ```console
      $ ridk install
    ```

    4. 重開一個 CMD 以便安裝 Jekyll 在適合的位置  

    ```console
      $ gem install jekyll bundler
    ```

    5. 最後輸入 jekyll -v 檢查是否順利安裝 Jekyll ， 這邊我安裝的版本是 jekyll 4.2.2  

    ```console
      $ jekyll -v
    ```

2. 到 [Chirpy Starte](https://github.com/cotes2020/chirpy-starter/generate) 產生自己的專案，專案名稱(Repository name)命名為 `<username>`.github.io (username 是你的使用者名稱)  
3. 將專案下載到你的電腦本機上，這邊我使用的是 [Github Desktop](https://desktop.github.com)。
4. 在執行專案之前，需要先安裝 Dependencies，打開 CMD 輸入 bundle。  

    ```console
      $ bundle
    ```

5. 接著使用[VS Code](https://code.visualstudio.com)打開該專案。在下方 TERMINAL 輸入 bundle exec jekylls  

    ```console
      $ bundle exec jekyll s
    ```

6. 最後可以打開在 Local 端的 Page 127.0.0.1:4000，以判斷是否執行成功。
   + 如果 _posts 裡有.md檔，可能導致執行失敗。

基本上到這邊環境都已經架設好了，接下來就是上傳到Github上面。  
  
## 部署至 Github 上

首先修改 _config.yml 裡的幾個項目，順便貼上自己的設定以供參考：  

+ lang：`zh-TW`（我自行修改[繁體中文](https://github.com/JinWei0811/jinwei0811.github.io/blob/main/_data/locales/zh-TW.yml)版本，需要放至 _data/_locales 裡）
+ timezone: `Asia/Taipei`
+ title: `XXX Blog`
+ url: 'https://`<username>`.github.io'
+ github username: `<username>`
+ social name: `<your name>`
+ social email: `<your email>`
+ social links: `https://github.com/<username>`
+ avatar: `/assets/img/sticker.jpg` 選一個大頭貼放至 /assets/img 裡  

如果你所使用的電腦版本為 Windows，需先一樣用 VS Code 開啟專案調整 Gemfile 系統版本，在Terminal輸入：

```console
      $ bundle lock --add-platform x86_64-linux
```

接著就可以用 Github Desktop 提交修改，並 Push 上 Github ，可以用網頁打開你的專案到 Actions 檢視 Build 情況。  
如果沒有出現任何Error，則可以在 `<username>`.github.io，檢視自己上傳的網頁。

## 開始撰寫文章

上傳成功後，則可以開始撰寫自己的Github文章囉！首先一樣用 VS Code 打開你的專案，找到 `_posts` 資料夾得位置，文章的格式為MD檔(MarkDown)有兩種方式可以新增檔案。
   1. 在 `_posts` 右鍵新增檔案，在最後檔案需加上 `.md` 後綴  
   2. 使用我上傳的 [範例檔案](https://github.com/JinWei0811/MarkDownExample/blob/main/2022-05-03-markdown.md) 

   但需要注意要加上標頭以便模板辨識標題、作者等資訊。專案在命名規則時請按照`西元年-月-日-網頁名稱.md`，就以這篇文章為例其命名為`2022-05-03-build_GitHubPage.md`。在命名上傳檔案後，盡量不要不要再修改檔案名稱，可能會導致找不到原先的網頁。


