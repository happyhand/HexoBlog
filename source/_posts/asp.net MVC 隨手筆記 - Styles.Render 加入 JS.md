---
title: asp.net MVC 隨手筆記 - Styles.Render 加入 JS
date: 2018-11-21 14:03:49
categories: 學習日誌
tags: asp.new MVC
---
## **使用 Styles.Render include JS、CSS**
### **include JS、CSS**
在 AppWeb/**BundleConfig** RegisterBundles function 中輸入
```
bundles.Add(new ScriptBundle("~/bundles/typename").Include("~/Scripts/filename"));
```
並在指定的 cshtml 中，使用 @Scripts.Render 即可使用
```
@Scripts.Render("~/bundles/typename")
```
以新增的 vue.js 為例
```
bundles.Add(new ScriptBundle("~/bundles/vue").Include("~/Scripts/vue.js"));
```
並於 Views/**_Layout.cshtml** 中加入
```
@Scripts.Render("~/bundles/vue")
```
![](https://imgur.com/hs2deeO.png)

*額外小補充
可使用 {version}、** *等模糊查詢功能*

### **include 指定資料夾下的所有 JS、CSS**
在 AppWeb/**BundleConfig** RegisterBundles function 中輸入
```
bundles.Add(newScriptBundle("~/bundles/typename").IncludeDirectory("~/Scripts/directoryname", "*.js", true));
```
舉個例子 >>>
新增 JS 檔案
![](https://imgur.com/itt99A8.png)

輸入代碼
```
bundles.Add(newScriptBundle("~/bundles/AllJS").IncludeDirectory("~/Scripts/MainJS", "*.js", true));
```
並在指定的 cshtml 中，使用 @Scripts.Render 即可使用
```
@Scripts.Render("~/bundles/AllJS")
```
![](https://imgur.com/Q3YKaV7.png)


*額外小補充
.js 檔案無法從 Views 資料夾下作引用
一定要放在 Scripts 資料夾下才可以*