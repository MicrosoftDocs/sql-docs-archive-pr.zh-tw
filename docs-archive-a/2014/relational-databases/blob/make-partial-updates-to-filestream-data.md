---
title: 對 FILESTREAM 資料進行部分更新 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 696c1a6421e14568877e24f015e5094395f1051b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707598"
---
# <a name="make-partial-updates-to-filestream-data"></a>對 FILESTREAM 資料進行部分更新
  應用程式會使用 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 對 FILESTREAM BLOB 資料進行部分更新。 [DeviceIoControl](https://go.microsoft.com/fwlink/?LinkId=105527) 函數會將此值以及從 [OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md) 中傳回的控制代碼傳遞給 FILESTREAM 驅動程式。 然後，此驅動程式會強制將目前 FILESTREAM 資料的伺服器端副本儲存至控制代碼所參考的檔案中。 如果應用程式在寫入此控制代碼之後發出 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 值，則最後一個寫入作業將會保存下來，而之前對此控制代碼所進行的寫入作業將會遺失。  
  
> [!NOTE]  
>  FILESTREAM 會仰賴 [SMB 通訊協定](https://go.microsoft.com/fwlink/?LinkId=112454) 進行遠端存取。  
  
## <a name="example"></a>範例  
 下列範例將示範如何使用 `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` 值，針對插入的 FILESTREAM BLOB 執行部分更新。  
  
> [!NOTE]  
>  本範例需要使用在 [建立啟用 FILESTREAM 的資料庫](create-a-filestream-enabled-database.md) 和 [建立儲存 FILESTREAM 資料的資料表](create-a-table-for-storing-filestream-data.md)中建立之啟用 FILESTREAM 的資料庫和資料表。  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_fsctl)]  
  
## <a name="see-also"></a>另請參閱  
 [使用 OpenSqlFilestream 存取 FILESTREAM 資料](access-filestream-data-with-opensqlfilestream.md)   
 [建立 FILESTREAM 資料的用戶端應用程式](create-client-applications-for-filestream-data.md)  
  
  
