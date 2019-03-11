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

**參考**
[MongoDB 官網文件](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/)