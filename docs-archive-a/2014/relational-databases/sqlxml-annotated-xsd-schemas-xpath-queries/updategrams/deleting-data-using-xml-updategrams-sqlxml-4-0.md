---
title: 使用 XML Updategram 刪除資料 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
author: rothja
ms.author: jroth
ms.openlocfilehash: d941005c71dc33dd8c4f5c5cc15f645cd0e68177
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598772"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>使用 XML Updategram 刪除資料 (SQLXML 4.0)
  當記錄實例出現在區塊中 **\<before>** ，但在區塊中沒有對應的記錄時，updategram 表示刪除作業 **\<after>** 。 在此情況下，updategram 會從資料庫中刪除區塊中的記錄 **\<before>** 。  
  
 下列是刪除作業的 Updategram 格式：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
       <ElementName />  
      [<ElementName .../>... ]  
   </updg:before>  
    [<updg:after>  
    </updg:after>]  
  </updg:sync>  
</ROOT>  
```  
  
 **\<after>** 如果 updategram 只執行刪除作業，您可以省略標記。 如果您沒有指定選擇性的 `mapping-schema` 屬性， **\<ElementName>** updategram 中指定的會對應至資料庫資料表，而子項目或屬性則會對應到資料表中的資料行。  
  
 如果在 updategram 中指定的元素符合資料表中的多個資料列，或不符合任何資料列，則 updategram 會傳回錯誤並取消整個 **\<sync>** 區塊。 Updategram 中的元素一次只能刪除一個記錄。  
  
## <a name="examples"></a>範例  
 本章節中的範例會使用預設對應 (也就是說，Updategram 中不會指定任何對應結構描述)。 如需使用對應架構之 updategram 的更多範例，請參閱[在 Updategram 中指定批註式對應架構 &#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
 若要使用下列範例建立工作範例，您必須符合[執行 SQLXML 範例的需求](../../sqlxml/requirements-for-running-sqlxml-examples.md)中所指定的需求。  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. 使用 Updategram 刪除記錄  
 下列 Updategram 會從 HumanResources.Shift 資料表刪除兩筆記錄。  
  
 在這些範例中，Updategram 不會指定對應結構描述。 因此 Updategram 會使用預設對應，其中元素的名稱會對應到資料表名稱，而屬性或子元素則會對應到資料行。  
  
 第一個 updategram 是以屬性為中心，而且會) 區塊中的兩個晚上和晚上晚上，識別兩個 (移位 **\<before>** 。 因為區塊中沒有對應的記錄 **\<after>** ，所以這是刪除作業。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
       <HumanResources.Shift ShiftID="4"  
                        Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift ShiftID="5"  
                        Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:before>  
  <updg:after>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  完成範例 B ( 「使用 updategram 插入多筆記錄」 ) [使用 XML updategram &#40;SQLXML 4.0&#41;插入資料](inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
2.  將上述 updategram 複製到 [記事本]，並將它儲存為與用來完成 ( 「使用 updategram 插入多筆記錄」 ) 在使用[XML updategram &#40;SQLXML 4.0&#41;插入資料](inserting-data-using-xml-updategrams-sqlxml-4-0.md)中所用的相同資料夾中的 Updategram-RemoveShifts.xml。  
  
3.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全性考慮](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
