---
title: Python 隨手筆記 - 安裝Django
date: 2018-11-26 12:09:53
categories: 學習日誌
tags: Python
---
## **安裝 Django**
在開始 Python 之旅前
咱們來安裝 **Django** 作為 Python 的 web 框架
#### **建立 Django 資料夾**
在開始一連串的安裝程序之前
我們先建立一個待會要安裝 Django 的資料夾
塔克用的是 **D:\WebProject\AppWeb\Django**
待會會以這個路徑為例子
#### **建立虛擬環境**
我們會建立一個虛擬環境供 Django 使用
打開命令提示字元 (cmd)，先將路徑指定到剛剛建立的 Django 資料夾
接著輸入建立虛擬環境的指令 (python -m venv 後面打上要建立的虛擬環境名稱)
```
python -m venv yourvirtualenvironmentname
```
塔克這邊的例子是
```
python -m venv venv
```
![](https://imgur.com/5H40UnX.png)

成功後就會看到原本 Python 安裝資料夾中，多了一個 venv 資料夾
![](https://imgur.com/SlDWDuT.png)

接著我們執行 ~venv/Scripts/activate，以進入到虛擬環境中
![](https://imgur.com/qYRZHqr.png)

成功後，會如下圖顯示 (前方會掛載自訂的虛擬環境名稱，如塔克所自訂的 **venv**)
![](https://imgur.com/eI6EgHY.png)

#### **安裝 Django**
接下來要開始安裝 **Django**
這邊塔克會先示範一個錯誤的情況
避免大家遇到跟我一樣的問題 Or2
首先輸入代碼，安裝 **Django**
```
pip install django==1.6.6
```
![](https://imgur.com/QqKBumK.png)

(圖中有提示要升級 **pip**，塔克這邊有跟著執行升級)
完成後，咱們來創建專案 !
輸入代碼以下代碼
```
python ~venv\Scripts\django-admin.py startproject yourprojectname
```
塔克這邊的例子是
```
python venv\Scripts\django-admin.py startproject Webapi
```
![](https://imgur.com/dqi8lB5.png)

噹噹 !! 發生錯誤了 !!
**AttributeError: module 'html.parser' has no attribute 'HTMLParseError'** 
後來 Google 了一下，發現是版本過舊所致
所以建議大家安裝前記得先到 [Django 官網](https://www.djangoproject.com/) 中看一下最新版本是多少 (會不會太晚講了 QAQ"aaa)
修改一下原本安裝得代碼，改成最新版本 
(這邊大家可以放心，Django 會先自動移除舊版本後，再安裝新版本)
```
pip install django==2.1.3
```
安裝好後，咱們重新創建專案 !
重新輸入剛剛得代碼
```
python ~venv\Scripts\django-admin.py startproject yourprojectname
```
![](https://imgur.com/EJuVs2t.png)

成功後，就會在 Django 資料夾中看見專案
![](https://imgur.com/q4shGGR.png)

**參考**
[Django Girls 教學](https://carolhsu.gitbooks.io/django-girls-tutorial-traditional-chiness/content/index.html)