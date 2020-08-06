---
title: 從舊版 SQL Server 匯入原生與字元格式資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- earlier versions [SQL Server], import and export data formats
- -V switch
- data formats [SQL Server], earlier versions
- previous versions [SQL Server], import and export data formats
ms.assetid: e644696f-9017-428e-a5b3-d445d1c630b3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 274c984d6ecec8af8f5bea27496450a45fc2f1df
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598378"
---
# <a name="import-native-and-character-format-data-from-earlier-versions-of-sql-server"></a>從舊版 SQL Server 匯入原生與字元格式資料
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您可以透過 **-V** 參數使用 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]bcp [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 、 **或** 匯入原生與字元格式資料。 **-V** 參數會讓 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用指定之舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料類型，而資料檔案格式將會與舊版中的資料檔案格式相同。  
  
 若要為資料檔案指定舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請使用 **-V** 參數搭配下列其中一個限定詞：  
  
|SQL Server 版本|Qualifier|  
|------------------------|---------------|  
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|**-V80**|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|**-V90**|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|**-V100**|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|**-V 110**|  
  
## <a name="interpretation-of-data-types"></a>資料類型的解譯  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新的版本支援一些新的類型。 如果您想要將新的資料類型匯入舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您必須以舊版 **bcp** 用戶端可讀取的格式儲存該資料類型。 下表摘述如何轉換新資料類型，以便與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相容。  
  
|SQL Server 2005 的新資料類型|與 6*x*版相容的資料類型|與 70 版相容的資料類型|與 80 版相容的資料類型|  
|---------------------------------------|-------------------------------------------|-----------------------------------------|-----------------------------------------|  
|`bigint`|`decimal`|`decimal`|*|  
|`sql_variant`|`text`|`nvarchar(4000)`|*|  
|`varchar(max)`|`text`|`text`|`text`|  
|`nvarchar(max)`|`ntext`|`ntext`|`ntext`|  
|`varbinary(max)`|`image`|`image`|`image`|  
|XML|`ntext`|`ntext`|`ntext`|  
|UDT<sup>1</sup>|`image`|`image`|`image`|  
  
 \*這個類型是原生支援的。  
  
 <sup>1</sup> UDT 表示使用者定義的類型。  
  
## <a name="exporting-using--v-80"></a>使用 -V 80 匯出  
 當您使用 **-V80**參數大量匯出資料時， `nvarchar(max)` 、 `varchar(max)` 、 `varbinary(max)` 、XML 和原生模式中的 UDT 資料會與4位元組前置詞一起儲存，就像、和資料一樣， `text` 而不是使用 `image` `ntext` 8 位元組前置詞，這是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本的預設值。  
  
## <a name="copying-date-values"></a>複製日期值  
 **bcp** 會使用 ODBC 大量複製 API。 因此，若要將日期值匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， **bcp** 會使用 ODBC 日期格式 (*yyyy-mm-dd hh:mm:ss*[ *.f...* ])。  
  
 **Bcp**命令會使用和值的 ODBC 預設格式來匯出字元格式資料檔案 `datetime` `smalldatetime` 。 例如，包含日期 `12 Aug 1998` 的 `datetime` 資料行會以字元字串 `1998-08-12 00:00:00.000` 大量複製到資料檔案。  
  
> [!IMPORTANT]  
>  `smalldatetime`使用**bcp**將資料匯入欄位時，請確定秒的值是00.000，否則作業將會失敗。 `smalldatetime` 資料類型只會保留最接近分鐘數的數值。 BULK INSERT 及 INSERT ...SELECT * FROM OPENROWSET(BULK...) 在這個案例中將不會失敗，但會截斷秒數值。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [SQL Server Database Engine 回溯相容性](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
