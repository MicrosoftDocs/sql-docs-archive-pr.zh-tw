---
title: 使用 IRow::GetColumns 和 ISequentialStream 擷取 BLOB 資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching BLOB data
- ISequentialStream interface
- GetColumns method
- BLOBs, fetching
ms.assetid: b57decda-b0c1-4ef6-8c81-491956de2890
author: rothja
ms.author: jroth
ms.openlocfilehash: d511460ce19ba09630cf0913de0515c197c64594
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687833"
---
# <a name="fetching-blob-data-using-irowgetcolumns-and-isequentialstream"></a><span data-ttu-id="d9150-102">使用 IRow::GetColumns 和 ISequentialStream 提取 BLOB 資料</span><span class="sxs-lookup"><span data-stu-id="d9150-102">Fetching BLOB Data Using IRow::GetColumns and ISequentialStream</span></span>
  <span data-ttu-id="d9150-103">下列函式會使用 **IRow::GetColumns** 和 **ISequentialStream** 來提取大型資料：</span><span class="sxs-lookup"><span data-stu-id="d9150-103">The following function uses **IRow::GetColumns** and **ISequentialStream** to fetch large data:</span></span>  
  
```  
void InitializeAndExecuteCommand()  
{  
    ULONG iidx;  
    WCHAR* wCmdString=OLESTR("SELECT * FROM MyTable");  
    // Do the initialization, create the session, and set command text.  
    hr = pICommandText->Execute(NULL, IID_IRow, NULL,   
                         &cNumRows,(IUnknown **)&pIRow)))  
    //Get 1 column at a time.  
    for(ULONG i=0; i < NoOfColumns; i++)  
      GetSequentialColumn(pIRow, iidx);  
    // Do the clean up.  
}  
HRESULT GetSequentialColumn(IRow* pUnkRow, ULONG iCol)  
{  
    HRESULT hr = NOERROR;  
    ULONG cbRead = 0;  
    ULONG cbTotal = 0;  
    ULONG cColumns = 0;  
    ULONG cReads = 0;  
    ISequentialStream* pIStream = NULL;  
    WCHAR* pBuffer[kMaxBuff]; //50 chars read by ISequentialStream::Read()  
    DBCOLUMNINFO* prgInfo;  
    OLECHAR* pColNames;  
    IColumnsInfo* pIColumnsInfo;  
    DBID columnid;  
    DBCOLUMNACCESS column;  
    hr = pUnkRow->QueryInterface(IID_IColumnsInfo,   
                            (void**) &pIColumnsInfo);  
    if(FAILED(hr))  
        goto CLEANUP;  
    hr = pIColumnsInfo->GetColumnInfo(&cColumns, &prgInfo, &pColNames);  
    // Get Column ID.  
    columnid = (prgInfo + (iCol))->columnid;  
    IUnknown* pUnkStream = NULL;  
    ZeroMemory(&column, sizeof(column));  
    column.columnid = prgInfo[iCol].columnid;  
    // Ask for Iunknown interface pointer.  
    column.wType = DBTYPE_IUNKNOWN;  
    column.pData = (LPVOID*) &pUnkStream;  
  
    hr = pUnkRow->GetColumns(1, &column);  
    // Get ISequentialStream from Iunknown pointer retrieved from  
    // GetColumns().  
    hr = pUnkStream->QueryInterface(IID_ISequentialStream,   
                                   (LPVOID*) &pIStream);  
    ZeroMemory(pBuffer, kMaxBuff * sizeof(WCHAR));  
    // Read 50 chars at a time until no more data.  
    do  
    {  
        hr = pIStream->Read(pBuffer, kMaxBuff, &cbRead);  
        cbTotal = cbTotal + cbRead;  
        // Process the data.  
    } while(cbRead > 0);  
  // Do the cleanup.  
    return hr;  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="d9150-104">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d9150-104">See Also</span></span>  
 [<span data-ttu-id="d9150-105">使用 IRow 擷取 BLOB 資料</span><span class="sxs-lookup"><span data-stu-id="d9150-105">Fetching BLOB Data Using IRow</span></span>](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
  
