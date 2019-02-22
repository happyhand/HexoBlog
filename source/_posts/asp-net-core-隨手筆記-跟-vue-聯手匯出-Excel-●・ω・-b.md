---
title: asp.net core 隨手筆記 - 跟 vue 聯手匯出 Excel (●・ω・)b
date: 2019-02-20 17:27:53
categories: 學習日誌
tags: asp.net core
---
## **安裝 NuGet 套件**
首先，先幫 **.net core** 安裝 Excel 所需套件 **DocumentFormat.OpenXml**
打開 nuget 套件管理介面，搜尋 **DocumentFormat.OpenXml**
這邊需要安裝兩個基本套件
1. DocumentFormat.OpenXml
2. DocumentFormat.OpenXml.DotNet.Core
![](https://imgur.com/qMdJv3I.png)

## **匯出 Excel**
範例中將會使用 **FileStreamResult** 回傳 Excel 資料串流
```
[HttpGet]
public FileStreamResult Get()
{
    #region 設定 Excel 要寫入的資料

    string[][] datas = new string[][]
    {
        new string[]{"一年甲班","王小明" },
        new string[]{"一年乙班","孫小美" }
    };

    #endregion 設定 Excel 要寫入的資料

    #region 建立 Excel 資料串流

    MemoryStream memoryStream = new MemoryStream();

    #region 建立 Excel 檔案

    using (var document = SpreadsheetDocument.Create(memoryStream, SpreadsheetDocumentType.Workbook))
    {
        #region 生成檔案

        WorkbookPart workbookPart = document.AddWorkbookPart();
        workbookPart.Workbook = new Workbook();

        WorksheetPart worksheetPart = workbookPart.AddNewPart<WorksheetPart>();
        worksheetPart.Worksheet = new Worksheet(new SheetData());

        Sheets sheets = workbookPart.Workbook.AppendChild(new Sheets());
        sheets.Append(new Sheet()
        {
            Id = workbookPart.GetIdOfPart(worksheetPart),
            SheetId = 1,
            Name = "Sheet Name"
        });

        #endregion 生成檔案

        #region 寫入資料

        SheetData sheetData = worksheetPart.Worksheet.GetFirstChild<SheetData>();
        //// 建立欄位
        Row fieldRow = new Row();
        fieldRow.Append(
            new Cell() { CellValue = new CellValue("Class"), DataType = CellValues.String },
            new Cell() { CellValue = new CellValue("Student"), DataType = CellValues.String }
        );
        sheetData.AppendChild(fieldRow);
        //// 輸入資料
        foreach (string[] data in datas)
        {
            Row row = new Row();
            row.Append(
                new Cell() { CellValue = new CellValue(data[0]), DataType = CellValues.String },
                new Cell() { CellValue = new CellValue(data[1]), DataType = CellValues.String }
            );
            sheetData.AppendChild(row);
        }

        #endregion 寫入資料
    }

    #endregion 建立 Excel 檔案

    #endregion 建立 Excel 資料串流

    #region 回傳資料串流

    memoryStream.Seek(0, SeekOrigin.Begin);
    return new FileStreamResult(memoryStream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet");

    #endregion 回傳資料串流
}
```

執行 api 後，就可以下載 Excel 了 (○｀･Д･´)9

## **vue-axios-blob 聯手出擊 (額外補充)**
因為專案因素
塔克使用 **vue** 當作前端架構
結果在使用 **post** 的時候
一直無法下載 Excel
後來餵狗之後才發現，原來 **ajax** 不支援文件回應部分
只能使用原生的 **<form\>** 提交表單或是尋求其他的方式
所以再次餵狗後，決定使用 **axios + blob** 的方式來下載 Excel

### **安裝 axios + blob**
**axios** 與 **blob** 的詳細解說再請大家餵狗，以避免誤導大家 :;(∩´﹏`∩);:
這邊就直接上使用方法了 !

#### **安裝 axios**
打開 **vscode** 終端機，輸入以下代碼，安裝 **axios**
```
npm install axios
```

安裝完後，輸入以下代碼，引入 axios 相關插件
```
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios，axios);
```
*額外小補充
在使用 **Vue.use** 時
**VueAxios** 需在 **axios** 前先引入*

#### **安裝 blob**
接著輸入以下代碼，安裝 **blob**
```
npm install blob
```

### **vue-axios-blob 範例使用**
在 api request post 的部分，輸入以下代碼
```
this.$http
  .post("Your post url", "Your post data", {
    headers: { "Content-Type": "application/json" }, //// 可根據傳遞資料的類型更換
    responseType: "blob" //// 回應類型為 blob
  })
  .then(respone => {
    const blob = new Blob([respone.data], { type: respone.data.type }); //// 建立 blob
    const downloadElement = document.createElement("a"); //// 建立 <a> 元素，用以連結 blob url
    const href = window.URL.createObjectURL(blob); //// 產生 blob url
    downloadElement.href = href; //// 放置 blob url
    downloadElement.download = "fileNmae.xlsx"; //// 下載檔案與檔案設置
    document.body.appendChild(downloadElement); //// 生成 <a> 元素
    downloadElement.click(); //// 執行下載
    document.body.removeChild(downloadElement); //// 下載完成，移除 <a> 元素
    window.URL.revokeObjectURL(href); //// 釋放 blob 對象
  });
```

執行 api 後，就可以讓 **vue** 利用 **axios + blob** 下載 Excel 了 (○｀･Д･´)9

## **ClosedXML 助陣! (額外補充)**
ClosedXML 是另一套 Eexcel 程式庫
其特色可以參考一下 [<span style="color:#6699FF;font-weight:bold">暗黑大</span>](https://blog.darkthread.net/blog/closedxml/) 的文章
這邊就直接說明如何使用 !

### **安裝 ClosedXML**
打開 nuget 套件管理介面，搜尋 **ClosedXML**，安裝套件
![](https://imgur.com/lJzsTtD.png)

### **ClosedXML  範例使用**
用前一個 **DocumentFormat.OpenXml** 為範本來修改成 **ClosedXML** 範例
因為 **ClosedXML** 能直接帶入的資料格式有點限制
所以會先把之前 **DocumentFormat.OpenXml** 範例中的資料替換成 **DataTable** 格式
下方範例請先忽略過資料格式的轉換
注重在建立 Excel 方面就好

輸入以下代碼
```
[HttpGet]
public FileStreamResult Get()
{
    #region 設定 Excel 要寫入的資料

    string[][] datas = new string[][]
    {
        new string[]{"一年甲班","王小明" },
        new string[]{"一年乙班","孫小美" }
    };

    DataTable dataTable = new DataTable();
    dataTable.Columns.Add("Class");
    dataTable.Columns.Add("Student");
    foreach (string[] data in datas)
    {
        DataRow dataRow = dataTable.NewRow();
        dataRow["Class"] = data[0];
        dataRow["Student"] = data[1];
        dataTable.Rows.Add(dataRow);
    }

    #endregion 設定 Excel 要寫入的資料

    #region 建立 Excel 資料串流

    MemoryStream memoryStream = new MemoryStream();

    #region 建立 Excel 檔案

    using (var workbook = new XLWorkbook())
    {
        var worksheet = workbook.Worksheets.Add(dataTable, "Sheet Name");
        workbook.SaveAs(memoryStream);
    }

    #endregion 建立 Excel 檔案

    #endregion 建立 Excel 資料串流

    #region 回傳資料串流

    memoryStream.Seek(0, SeekOrigin.Begin);
    return new FileStreamResult(memoryStream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet");

    #endregion 回傳資料串流
}
```

其中會發現，原本很大一串建立 Excel 資料的 code
**ClosedXML** 都直接幫我們做好了，是不是很方便呢 ! (○｀･Д･´)9
![](https://imgur.com/LDBZPxY.png)

**參考**
[jQuery ajax](http://api.jquery.com/jquery.ajax/)
[axios github](https://github.com/axios/axios)
[ASP.NET Core 教學 - Open XML SDK 匯出 Excel](https://blog.johnwu.cc/article/asp-net-core-export-to-excel.html) 
[Vue亂搞系列之axios發起表單請求](https://www.jianshu.com/p/b22d03dfe006)
[令人驚豔的Excel程式庫 - ClosedXML](https://blog.darkthread.net/blog/closedxml/)
[ClosedXML github](https://github.com/ClosedXML/ClosedXML)