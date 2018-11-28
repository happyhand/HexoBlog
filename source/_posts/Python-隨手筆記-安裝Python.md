---
title: Python 隨手筆記 - 安裝Python
date: 2018-11-26 10:36:08
categories: 學習日誌
tags: Python
---
## **安裝 Python**
於 [Python官網下載頁](https://www.python.org/downloads/) 下載 Python 套件
![](https://imgur.com/hQqjVob.png)

安裝套件，這邊要注意一下
請將 **"Add Python 3.7 to Path"** 選項勾起，讓系統設定好環境變數
(因為安裝軟體預設是沒勾起，塔克當初忽略它，結果一直安裝不好，搞好久 Or2)
![](https://imgur.com/UAFFtpR.png)

安裝好後，請打開命令提示字元 (cmd)，輸入以下指令，測試有沒有成功安裝版本
```
python --version
```
![](https://imgur.com/BXKTrIk.png)

## **跟世界說聲 Hello**
利用筆記本新創一個檔案 **hello.py** (記得另存新檔成 .py 檔案唷)
![](https://imgur.com/dEiPJ2p.png)

永遠都要先跟世界說 Hello 唷 😃
```
print("Hello World !");
```
打開命令提示字元 (cmd)，輸入以下指令，呼叫剛剛的檔案，跟世界說聲 Hello !
```
python hello.py
```
![](https://imgur.com/yNztjar.png)

*額外小補充
安裝完 Python 後，記得要重開機，環境變數才會生效唷 !
(當初塔克又卡在這邊很久 Or2)*