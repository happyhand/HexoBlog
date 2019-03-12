---
title: MongoDB 隨手筆記 - 建立 MongoDB 服務
date: 2019-03-11 23:17:58
categories: 學習日誌
tags: MongoDB
---
## **安裝 MongoDB**
首先到 [MongoDB 官網](https://www.mongodb.com/download-center/community) 下載 MongoDB 套件
安裝步驟在 Google 上有很多範例，再請大家餵狗一下
這邊也提供了 [MongoDB 官網安裝文件](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/) 給大家參考一下

## **建立 MongoDB 資料夾、config**
因為塔克有習慣把資料分類，所以會把 DB 建立在指定的資料夾中
首先先創建出指定的資料夾，並在此資料夾中新增
1. data 資料夾
2. data\db 資料夾
3. log 資料夾
4. mongo.config

![](https://imgur.com/JEQLMiK.png)

![](https://imgur.com/FEqvJ6G.png)

mongo.config 中的配置，大家有興趣的話，可以參考 [MongoDB 官網 Config 設定](https://docs.mongodb.com/manual/reference/configuration-options/)
```
systemLog:
   destination: file
   path: D:\MongoDB\log\mongo.log
   logAppend: true
storage:
   dbPath: D:\MongoDB\data\db
   directoryPerDB: true
net:
   bindIp: 127.0.0.1
   port: 27117
processManagement:
   windowsService:
      serviceName: MyMongoServiceDB
      displayName: MyMongoServiceDB
```
![](https://imgur.com/FBuHdS9.png)

## **建立 MongoDB 服務**
打開 **命令提示字元** (注意!這邊需要用**系統管理員**模式開啟!)
將路徑指定到 MongoDB 執行檔資料夾 (C:\Program Files\MongoDB\Server\4.0\bin)
輸入以下代碼
```
mongod --config d:\MongoDB\mongo.config --install
```
![](https://imgur.com/vZJyZja.png)
啟動服務
```
net start MyMongoServiceDB
```

![](https://imgur.com/cWkQeZh.png)

打開 **工作管理員** > **服務**
就可以看到剛剛啟動的 MongoDB 服務了 (ゝ∀･)b
![](https://imgur.com/r3rWsRy.png)

若想停止服務、刪除服務的話
可以輸入以下代碼
**停止服務**
```
net stop MyMongoServiceDB
```
**刪除服務**
```
sc delete MyMongoServiceDB
```
![](https://imgur.com/TPBR3uX.png)

## **額外小補充**
如果大家有跟我碰到一樣的雷，下面解法給大家做參考一下!

狀況 1.
```
Requested option conflicts with current storage engine option for directoryPerDB; 
you requested true but the current server storage is already set to false and cannot be changed, terminating
```
請清除掉 **mongo.config** 中的 **dbPath** 路徑下的所有檔案
以塔克的範例為例，則是清除掉 **data/db** 資料夾下的所有檔案

狀況 2.
```
xxx requires an absolute file path with Windows services
```
這邊 **xxx** 可能會是 **config** 或是 **log** 或是其他類型
其原因基本上都是路徑設定錯誤
有可能是在 **mongo.config** 寫錯了路徑或是在路徑上加上了 **雙引號 - "**
或者是在 **命令提示字元** 中所執行的 **mongod --config d:\MongoDB\mongo.config --install** 這段代碼
路徑有設定錯誤

**參考**
[MongoDB 官網文件](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/)