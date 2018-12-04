---
title: Python 隨手筆記 - 把 Django 丟到雲端去 (╯°▽°)╯
date: 2018-12-04 16:43:08
categories: 學習日誌
tags: Python
---
## **找個雲端好夥伴 - Google Cloud Platform (GCP)**
把 Django 部屬到雲端去有很多方式
塔克這邊選擇用 **GCP** 中的 **App Engine** 來部屬 Django
在開始部屬 Django 步驟之前
有幾點需事先準備好
1. 建立 GCP 帳號
2. [下載 GCP 的專用套件 - Cloud SDK](https://cloud.google.com/sdk/)
3. 設定 GAE

### **建立 GCP 帳號**
估狗上已經有很多教學範例
這邊就不贅述了
再請大家先餵狗一下唷 (･ω･)

*額外小補充
真找不到教學的朋友，可以參考這位大大的教學唷
[GCP_如何用Google Cloud Platform創建Server_帳號申請、Server建立](http://kuanzi9487.blogspot.com/2017/09/gcpgoogle-cloud-platformserverserver.html)*

### **下載 GCP 的專用套件**
進入 [Cloud SDK 下載頁面](https://cloud.google.com/sdk/)
選擇系統版本下載並安裝
安裝的部分也是毫無懸念地，一路給它下一步、下一步安裝到底
![](https://imgur.com/tdtfAb3.png)

安裝好後，系統會自動開啟 **Google Cloud SDK Shell**
(若沒有自動開啟，可以自行開啟 **Google Cloud SDK Shell**)
![](https://imgur.com/3FFOPKO.png)

如果之前有像塔克一樣有先設定過的話
會像畫面中顯示兩個選項
1. 採用預設 config
2. 建立新的 config

如果之前沒有設定過的話
再請輸入以下指令，初始化 gcloud 設定
```
gcloud init
```

這邊塔克都是延續上一次設定
**帳號選擇**
![](https://imgur.com/PIXYAkW.png)

**專案ID選擇**
![](https://imgur.com/XTPa7Sb.png)

**是否選擇區域**
![](https://imgur.com/VZkfjaD.png)

**選擇亞洲區域 (這邊請選擇適合自己的區域)**
![](https://imgur.com/sotp8WE.png)

設定好囉，就可以開始使用 **Google Cloud SDK Shell** 來上傳 Django 到 **GAE** 了 !
### **設定 GAE**
回到 GCP 的網頁
點擊 **主選單**，開啟下拉選單，選擇 **App Engine**，設定部屬環境
![](https://imgur.com/IppTm98.png)

接著開啟語言選擇
![](https://imgur.com/8CNZE7F.png)

我們這邊選擇 Python 語言
![](https://imgur.com/Y0wetxP.png)

選擇一個適合的區域
![](https://imgur.com/m0yoU48.png)

完成設定後，GCP 會詢問要不要進入教學課程，有興趣的朋友可以看一下唷 !
![](https://imgur.com/EKtaFx6.png)

## **GOGO ! 部屬 Django 到雲端去 !!**
在開始部屬到雲端前
請大家先準備好自己的 Django 專案
如果還沒準備好或不知道怎麼建立 Django 專案的
可以參考塔克之前寫的 [Python 隨手筆記 - 用 Django 作個網頁吧 !](https://happyhand.github.io/2018/11/28/Python-%E9%9A%A8%E6%89%8B%E7%AD%86%E8%A8%98-%E7%94%A8-Django-%E4%BD%9C%E5%80%8B%E7%B6%B2%E9%A0%81%E5%90%A7/) 文章做練習

### **加入 app.yaml**
建立好基本專案後，也確定本地端伺服器 (**http://127.0.0.1:8000/**) 可以正常運行後
在建立的專案底下，新增 app.yaml 檔案
並輸入以下代碼
```
runtime: python37

handlers:
- url: /static
  static_dir: static/

- url: /.*
  script: auto
```
![](https://imgur.com/Zb6ShmK.png)

app.yaml 的設定可以參考 [app.yaml Reference](https://cloud.google.com/appengine/docs/standard/python3/config/appref)
### **加入 main.py**
在建立的專案底下，新增 main.py 檔案
並輸入以下代碼
```
from mysite.wsgi import application
app = application
```
![](https://imgur.com/eexbczx.png)

GAE 預設會依照根目錄下 **main.py** 檔案中的 app 變數，作為 Django 網站程式的介面
### **修改 setting.py**
打開 **yourprojectname/setting.py** (塔克範例是 **Webapi/setting.py**)
先進入到
修改 **ALLOWED_HOSTS** 設定
```
ALLOWED_HOSTS = ['*']
```
新增 **STATIC_ROOT** 設定，以便建立靜態檔案
```
STATIC_ROOT = 'static'
```
![](https://imgur.com/WoySscN.png)
.
.
.
![](https://imgur.com/S6bhVWk.png)
### **以 Google Cloud SDK Shell 執行，進入虛擬環境**
打開 **Google Cloud SDK Shell** 
依專案設定進入虛擬環境 (以塔克的範例是 **~/venv/Scripts/activate**)
並將路徑指定到專案下 (以塔克的範例是 **~/Django/Webapi**)
### **設定資料庫**
若想看看在專案中有哪些資料有新增或異動過的話
可以在 **Google Cloud SDK Shell** 中，輸入以下代碼
```
python manage.py makemigrations
```
接著輸入以下代碼，以初始化或更新設定資料庫
```
python manage.py migrate
```
![](https://imgur.com/argVuot.png)

### **編制靜態檔案**
繼續在 **Google Cloud SDK Shell** 中
輸入以下代碼編制靜態檔案
```
python manage.py collectstatic
```
這個指令會根據 settings.py 中的 STATIC_ROOT 的值來編製
同時 app.yaml 也指定 /static 對應的靜態檔案目錄，讓 GAE 來服務靜態檔案
![](https://imgur.com/tB4z5oi.png)

### **測試本地伺服器**
繼續在 **Google Cloud SDK Shell** 中，輸入以下代碼測試網站是否正常
```
python manage.py runserver
```
輸入網址 **http://127.0.0.1:8000/** ，成功後將會看到 Django 的歡迎頁面
### **建立 requirements.txt**
繼續在 **Google Cloud SDK Shell** 中，輸入以下代碼建立 **requirements.txt**
```
pip freeze > requirements.txt
```
requirements.txt 將會告訴 GAE 我們需要用到那些應用程式
如果沒有這個檔案的話，網頁會發生 502 錯誤唷 !

*額外小補充
如果有朋友像塔克一樣習慣用 **VSCode** 下指令的話
在這個步驟強烈建議使用 **Google Cloud SDK Shell** 來建立 **requirements.txt**
或者是自己手動建立 txt 檔，並輸入相關代碼
因為用 **VSCode** 輸入指令的話，會造成 GAE 無法辨識 **requirements.txt**
導致網站無法 deploy*

### **往雲端丟丟丟 (ﾉ≧∇≦)ﾉ**
繼續在 **Google Cloud SDK Shell** 中，輸入以下代碼
```
gcloud app deploy
```
這時候系統會顯示要上傳得相關設定是否正確
![](https://imgur.com/ls6eFK4.png)

檢視後，若沒問題，就可以正式上傳
成功上傳後，可以直接從 **Google Cloud SDK Shell** 中，輸入以下代碼
```
gcloud app browse
```
![](https://imgur.com/hXLcCwu.png)

或是直接開啟網頁 **http://yourprojectid.appspot.com**
沒問題的話，就可以看到 Django 跟你 say hello 囉 !

**參考**
[GCP_如何用Google Cloud Platform創建Server_帳號申請、Server建立](http://kuanzi9487.blogspot.com/2017/09/gcpgoogle-cloud-platformserverserver.html)
[部署 Django 2 至 Google App Engine 第二代標準環境教學](https://blog.uccloud.com.tw/2018/10/28/%E9%83%A8%E7%BD%B2-django-2-%E8%87%B3-app-engine-2nd-%E6%A8%99%E6%BA%96%E7%92%B0%E5%A2%83%E6%95%99%E5%AD%B8/)
[app.yaml Reference](https://cloud.google.com/appengine/docs/standard/python3/config/appref)