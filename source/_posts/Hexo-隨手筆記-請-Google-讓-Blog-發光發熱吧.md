---
title: Hexo 隨手筆記 - 請 Google 讓 Blog 發光發熱吧 !
date: 2018-11-29 14:11:20
categories: 學習日誌
tags: Hexo
---
## **讓 Google 找到 Blog** （๑✧∀✧๑）
為了讓 Google 可以更加靈活地搜尋到自己的 Blog
我們可以提供 **Sitemap** 檔案給 Google 進行讀取分析
這樣有助於別人可以透過 Google 搜尋到自己的 Blog
(以下操作方式均在 **VS Code** 開發環境中執行)

### **安裝 hexo sitemap 套件**
首先輸入以下代碼安裝 **hexo-generator-sitemap** 套件
```
npm install hexo-generator-sitemap --save
```
![](https://imgur.com/GoTWyBb.png)

成功後，可以在 package.json 檔案中，看到剛剛新增的 **hexo-generator-sitemap** 套件
![](https://imgur.com/zf6j6Yc.png)

### **加入 Sitemap 路徑**
打開主程序中的 **_config.yml**，並輸入以下代碼
```
#Sitemap
sitemap:
    path: sitemap.xml
```
![](https://imgur.com/NlLx6sp.png)

### **創建 Sitemap 檔案**
接著啟動本地伺服器
```
hexo s -p
```
![](https://imgur.com/BfU6ocb.png)

於網址中最後輸入 **/sitemap.xml**
以塔克為例：http://localhost:4000/sitemap.xml
就會看到 **Sitemap** 檔案內容
![](https://imgur.com/aqekfFR.png)

### **向 Google 申請 Blog Search**
首先打開 [**Google Search Console**](https://search.google.com/search-console/welcome) (在此之前請先申辦一個 Google 帳號並登入唷 !)
接著把 Blog 的主頁網址輸入
以塔克為例：https://happyhand.github.io/
![](https://imgur.com/TuMppsH.png)

提交後會看到 Google 請我們驗證網頁
![](https://imgur.com/ehzmHGT.png)

*額外小補充
是輸入主頁網址，不是剛剛的 sitemap.xml 網址唷 !!!
不然等等驗證會一直找不到網頁 !!!
不要像塔克一樣笨笨的，卡到快懷疑人生了* ╥﹏╥
### **向 Google 驗證 Blog**
總共有5種驗證方式
塔克選擇以 **HTML 標記** 為驗證方式
而這個驗證方式說簡單很簡單，說麻煩也挺麻煩的 (當時塔克又差點懷疑人生了 Or2)
簡單是說，只要把 **HTML 中繼標記** (如下圖紅框) 添加到網站首頁的 < head > 至 < body > 區間中即可驗證
![](https://imgur.com/VKHqAGa.png)

麻煩的是，因為 Hexo 的主題框架有很多種，偏偏每一種的添加方式又不太一樣
這邊塔克也是愛莫能助，只能提供塔克使用的主題 - [**Melody**](https://github.com/Molunerfinn/hexo-theme-melody) 給大家做參考

### **在 Blog 中添加 Google HTML 標記驗證 (以主題 - Melody 為例)**
打開 ~/themes/Melody/layout/includes/layout.pug
找到 **doctype html** 設定
在 **head** 以及 **body** 中添加 **HTML 中繼標記**
```
meta(name="google-site-verification" content="85ut1Jqu7TICdlVpdg-R5Fu5dKwOj5tKHDS2-drMK7k")
```
![](https://imgur.com/deS99VU.png)

接著打開 ~/themes/Melody/layout/includes/slide/layout.pug
以相同的方式添加 **HTML 中繼標記**
這邊塔克就不贅述了
接著 delpoy Blog，讓 Google 可以找到我們所添加的 **HTML 中繼標記**
再回到 Google 驗證的頁面提交驗證
成功後如下圖顯示：
![](https://imgur.com/Zu8lL44.png)

### **提交 Sitemap 網頁**
前往資源設定頁面後
打開 **主選單**，選擇 **Sitemap**，進入提交畫面
輸入 Sitemap 網址 (就是 **https://yourblogurl/sitemap.xml** ，通常只要輸入 **sitemap.xml** 就好)
按下提交
![](https://imgur.com/B91C1Mn.png)

成功後，就等著 Google 幫我們去做網頁搜尋分析囉 (✪▽✪)y
![](https://imgur.com/n8yH2MG.png)

**參考**
[Sitemap 說明](https://support.google.com/webmasters/answer/156184)
[Hexo Sitemap Github](https://github.com/hexojs/hexo-generator-sitemap)