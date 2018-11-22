---
title: asp.net MVC 隨手筆記 - 使用 Open Iconic 加入圖示
date: 2018-11-22 17:21:46
categories: 學習日誌
tags: asp.new MVC
---
# 使用 Open Iconic 添加網頁圖示
於 [OPENICONIC 官網](https://useiconic.com/open/) 下載圖示壓縮檔
![image alt](https://imgur.com/aSlElQC.png)

下載並解壓縮後，於 ~/open-iconic-master/font/**css** 中提取所需的 css 檔案
並將其檔案放置 asp.net MVC **~/Content** 資料夾中 (小編這邊提取的是**open-iconic-bootstrap.min.css**)
以及 ~/open-iconic-master/font/**fonts** 中提取所有檔案
並將其檔案放置 asp.net MVC **~/fonts** 資料夾中
![image alt](https://imgur.com/z657352.png)

於 [OPENICONIC 官網](https://useiconic.com/open/) 挑選要加入的圖示
並點擊圖示以彈跳出代碼範例
![image alt](https://imgur.com/3CVUdtd.png)

因為小編提取的是 **bootstrap.min.css**
所以採用 **Bootstrap Icon Font** 代碼
並於要顯示的 html 加入代碼 (這邊以 Home Page 為例)
```
@{
    ViewBag.Title = "Home Page";
}

<div>
    <span> Hello World</span>
    <span class="oi oi-heart"></span>
</div>
```
即可顯示圖示
![image alt](https://imgur.com/yzSoLCy.png)

**參考**
[OPENICONIC 官網](https://useiconic.com/open/)