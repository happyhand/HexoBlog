---
title: asp.net core 隨手筆記 - 使用 IIS 架設 .net core API 站台
date: 2019-02-12 15:49:52
categories: 學習日誌
tags: asp.net core
---
## **安裝 .NET Core 裝載套件組合**
於[官網](https://docs.microsoft.com/zh-tw/aspnet/core/host-and-deploy/iis/?view=aspnetcore-2.2#install-the-net-core-hosting-bundle)下載 .net Core 裝載套件組合
![](https://imgur.com/NCQTKwl.png)

安裝套件
![](https://imgur.com/R4GYD2g.png)

## **架設 .net core API 站台**
於 **IIS** 設定 API 站台
這邊要注意幾個要點
1. 需使用 **發行** 發佈檔案
![](https://imgur.com/PmudzhH.png)

2. 實體路徑須設定至 **publish** 位置 
![](https://imgur.com/oHQKZmg.png)

3. 於 **hosts** config 中加入本地 domain ```127.0.0.1 www.appnetcore.test```
(host config 可於 **C:\Windows\System32\drivers\etc** 中找到)
![](https://imgur.com/ZuOucG9.png)

以上都設定完後，即可測試 api 是否成功 (*ゝ∀･)v