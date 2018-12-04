---
title: Python 隨手筆記 - 用 Django 作個網頁吧 !
date: 2018-11-28 18:19:56
categories: 學習日誌
tags: Python
---
## **工欲善其事，必先利其器 !**
在開始建立個人網頁前
我們先來找個合適的 IDE or 文本編輯器來編譯我們的專案 
(專案將會延續 [Python 隨手筆記 - 安裝Django](http://happyhand.github.io/2018/11/26/Python-隨手筆記-安裝Django/) 的設定作說明)
### **來試試 VS Code**
在工具方面，塔克是使用 [VS Code](https://code.visualstudio.com/) 來做為 Python 的文本編輯器
有興趣的朋友可以參考一下
這邊會再重新複習上一個章節 [Python 隨手筆記 - 安裝Django](http://happyhand.github.io/2018/11/26/Python-隨手筆記-安裝Django/) 所進行的步驟
已經熟悉的朋友可以直接跳過，直接往下一個步驟 [**讓伺服器跑起來 !**](https://happyhand.github.io/2018/11/28/Python-%E9%9A%A8%E6%89%8B%E7%AD%86%E8%A8%98-%E7%94%A8-Django-%E4%BD%9C%E5%80%8B%E7%B6%B2%E9%A0%81%E5%90%A7/#%E8%AE%93%E4%BC%BA%E6%9C%8D%E5%99%A8%E8%B7%91%E8%B5%B7%E4%BE%86) 進行
#### **安裝 VS Code**
首先先到 [VS Code 官網](https://code.visualstudio.com/) 安裝 **VS Code**
![](https://imgur.com/mBDSgJC.png)

接著以 VS Code 開啟事先建立好的 Django 資料夾
![](https://imgur.com/3EpE4gd.png)

在執行 Python 相關動作前，我們先來安裝 Python 套件
![](https://imgur.com/86IO6cu.png)

#### **創建虛擬環境**
在 VS Code 環境中打開終端機 (快捷鍵是 **Ctrl+\`**)
一樣輸入創建虛擬環境的代碼
```
python -m venv yourvirtualenvironmentname
```
塔克這邊的例子是
```
python -m venv venv
```
![](https://imgur.com/WGLsB7Q.png)

接著就會看到原本 Django 資料夾中，多了一個 venv 資料夾
![](https://imgur.com/SlDWDuT.png)

接著我們執行 **~/venv/Scripts/activate**，以進入到虛擬環境中
這邊塔克有遇到 **終端機 powershell** 無法執行的問題 (如圖中的紅色提示)
![](https://imgur.com/v6Dpn5H.png)

此時我們打開 powershell (記得使用**管理員模式**)
輸入以下指令，並選擇 **Y** 即可正常執行 **~/venv/Scripts/activate** 指令
```
Set-ExecutionPolicy RemoteSigned
```
![](https://imgur.com/sEX1l5D.png)

成功後，前方會掛載自訂的虛擬環境名稱，如塔克所自訂的 **venv**
![](https://imgur.com/ZEQQOZQ.png)

#### **安裝 Django 並創建專案**
接著安裝 **Django** (記得輸入最新版本唷)
```
pip install django==2.1.3
```
![](https://imgur.com/fqlxtaT.png)

完成後，輸入以下代碼創建專案
```
python ~\venv\Scripts\django-admin.py startproject yourprojectname
```
塔克這邊的例子是
```
python venv\Scripts\django-admin.py startproject Webapi
```
![](https://imgur.com/q8KrHl9.png)

## **讓伺服器跑起來 !**
首先來看看 manage.py 這個檔案
manage.py 是 Django 提供的命令列工具，我們稍後會一直跟它打交道
詳細的說明可以參考 [Django 官網說明](https://docs.djangoproject.com/en/2.1/ref/django-admin/) 以及 [Django Girls 學習指南](https://djangogirlstaipei.gitbooks.io/django-girls-taipei-tutorial/django/project_and_app.html)
輸入以下代碼，來跑跑看伺服器吧 ! (記得先將終端機目錄指定到剛剛建立的專案中唷!)
```
python manage.py runserver
```
![](https://imgur.com/9mzZp2T.png)

成功後會顯示出 **Starting development server at http://127.0.0.1:8000/**
開啟本地網頁 http://127.0.0.1:8000/ ，即可看到成功頁面
![](https://imgur.com/ctlOnPh.png)

## **來個網頁應用程式吧 !**
開始來做個網頁吧
首先先來創建個 Application
回到 VS Code 輸入以下指令 (可以使用 **Ctrl+C** 讓終端機回到輸入指令的模式)
```
python manage.py startapp yourapplicationname
```
塔克這邊的例子是
```
python manage.py startapp ApiService
```
成功後，就可以在介面中看到創建好的 Application
![](https://imgur.com/39s1CBp.png)

接著打開 **~Webapi/settings.py**
調整一下裡面的屬性，讓 Django 管理剛創建的 Application
```
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'ApiService', #加上自己的應用程式，提供給 Django 管理
]
```
## **HTTP request & HTTP response**
打開 **~/ApiService/views.py**
創建一個 **hello_world** 的 Http request
呼叫後，會回應 **Hello World!**
輸入以下代碼
```
from django.http import HttpResponse

def hello_world(request):
    return HttpResponse("Hello World!")
```
接著打開 **~/Webapi/urls.py**
import 剛剛建立的 function
```
from ApiService.views import hello_world
```
並在 **urlpatterns** 下加入路徑
```
path('hello', hello_world),
```
代碼看起來會像這樣
```
from django.contrib import admin
from django.urls import path
from ApiService import hello_world

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello', hello_world),
]
```
接著在啟動伺服器
網址輸入 **http://127.0.0.1:8000/hello**
就可以看到回覆的 **Hello World!**
![](https://imgur.com/VyPO03W.png)

*額外小補充
在 **path('hello', hello_world)** 路徑設定中
如果要對其路徑進行正則表達式
如 **r'^hello/$', hello_world**
那麼就要先 import **re_path**
**from django.urls import re_path**
在將 **path** 替換成 **re_path**
**re_path(r'^hello/$', hello_world)**
*

## **建立網頁**
在我們專案中，先建立一個放置網頁的資料夾 **templates**
並在此資料夾中，新增一個 **hello_world.html**
![](https://imgur.com/MrgCC0S.png)

在 hello_world.html 中，輸入以下代碼
```
<!-- hello_world.html -->

<!DOCTYPE html>
<html>
    <head>
        <title>I come from template!!</title>
        <style>
            body {
               background-color: lightyellow;
            }
            em {
                color: LightSeaGreen;
            }
        </style>
    </head>
    <body>
        <h1>Hello World!</h1>
        <em>{{ current_time }}</em>
    </body>
</html>
```
接著回到 **~/ApiService/views.py** 中，修改一下代碼，內容如下
```
from django.shortcuts import render
from django.http import HttpResponse
from datetime import datetime

def hello_world(request):
    return render(request, 'hello_world.html', {
        'current_time': str(datetime.now()),
    })
```
接著再回到 **~Webapi/settings.py**，調整 **TEMPLATES** 設定
修改一下 **DIRS**，內容如下
```
'DIRS': [os.path.join(BASE_DIR, 'templates').replace('\\', '/')],
```
重新啟動伺服器後，就可以看到網頁不再是單純的文字回覆囉 !
![](https://imgur.com/Bxv1zja.png)


**參考**
[VS Code 官網](https://code.visualstudio.com/) 
[PowerShell 執行出錯](http://asika.windspeaker.co/post/3500-powershell-remotesigned)
[Django 官網文件](https://docs.djangoproject.com/en/2.1/)
[Django 網站框架 (Python)](https://developer.mozilla.org/zh-TW/docs/Learn/Server-side/Django)
[Django Girls 學習指南](https://djangogirlstaipei.gitbooks.io/django-girls-taipei-tutorial/)