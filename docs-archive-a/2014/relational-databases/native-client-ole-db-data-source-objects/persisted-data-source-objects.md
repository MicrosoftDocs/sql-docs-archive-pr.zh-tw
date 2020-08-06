---
title: 保存的資料來源物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB data source objects [SQL Server Native Client]
- data source objects [OLE DB]
- SQL Server Native Client OLE DB provider, persisted data source objects
- persisted data source objects
ms.assetid: dfdacc81-42fe-4f20-8969-bed1f743defe
author: rothja
ms.author: jroth
ms.openlocfilehash: d6d115b6640c910a70a9a29a36607a122f650c3c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591999"
---
# <a name="persisted-data-source-objects"></a><span data-ttu-id="82f3a-102">保存的資料來源物件</span><span class="sxs-lookup"><span data-stu-id="82f3a-102">Persisted Data Source Objects</span></span>
  <span data-ttu-id="82f3a-103">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者支援使用**IPersistFile**介面保存的資料來源物件。</span><span class="sxs-lookup"><span data-stu-id="82f3a-103">The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider supports persisted data source objects with the **IPersistFile** interface.</span></span>  
  
## <a name="examples"></a><span data-ttu-id="82f3a-104">範例</span><span class="sxs-lookup"><span data-stu-id="82f3a-104">Examples</span></span>  
 <span data-ttu-id="82f3a-105">**A. 保存資料來源初始化：**</span><span class="sxs-lookup"><span data-stu-id="82f3a-105">**A. Persist data source initialization:**</span></span>  
  
 <span data-ttu-id="82f3a-106">這個範例會示範一個函數，此函數會保存定義伺服器和資料庫的資料來源初始化屬性，以及使用 Windows 驗證模式來進行連接。</span><span class="sxs-lookup"><span data-stu-id="82f3a-106">This example shows a function that persists data source initialization properties defining a server, database, and the use of the Windows Authentication Mode for connection.</span></span> <span data-ttu-id="82f3a-107">伺服器名稱和資料庫名稱會在此函式的 *pLocation* 和 *pDatasource* 參數中接收。</span><span class="sxs-lookup"><span data-stu-id="82f3a-107">The server name and database name are received in the *pLocation* and *pDatasource* parameters of the function.</span></span>  
  
```  
HRESULT SetAndSaveInitProps  
    (  
    IDBInitialize* pIDBInitialize,  
    WCHAR* pDataSource,  
    WCHAR* pCatalog,  
    BOOL bUseWinNTAuth  
    )  
    {  
    const ULONG     nProps = 4;  
    ULONG           nSSProps;  
    ULONG           nPropSets;  
    ULONG           nProp;  
    IDBProperties*  pIDBProperties  = NULL;  
    IPersistFile*   pIPersistFile   = NULL;  
    DBPROP          aInitProps[nProps];  
    DBPROP*         aSSInitProps    = NULL;  
    DBPROPSET*      aInitPropSets   = NULL;  
    HRESULT         hr;  
  
        nSSProps = 0;  
        nPropSets = 1;  
  
    aInitPropSets = new DBPROPSET[nPropSets];  
  
    // Initialize common property options.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        VariantInit(&aInitProps[nProp].vValue);  
        aInitProps[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        aInitProps[nProp].colid = DB_NULLID;  
        }  
  
    // Level of prompting that will be done to complete the connection  
    // process.  
    aInitProps[0].dwPropertyID = DBPROP_INIT_PROMPT;  
    aInitProps[0].vValue.vt = VT_I2;  
    aInitProps[0].vValue.iVal = DBPROMPT_NOPROMPT;       
  
    // Server name.  
    aInitProps[1].dwPropertyID = DBPROP_INIT_DATASOURCE;      
    aInitProps[1].vValue.vt = VT_BSTR;  
    aInitProps[1].vValue.bstrVal = SysAllocString(pDataSource);  
  
    // Database.  
    aInitProps[2].dwPropertyID = DBPROP_INIT_CATALOG;  
    aInitProps[2].vValue.vt = VT_BSTR;  
    aInitProps[2].vValue.bstrVal = SysAllocString(pCatalog);  
  
    aInitProps[3].dwPropertyID = DBPROP_AUTH_INTEGRATED;  
    if (bUseWinNTAuth == TRUE)  
    {  
        aInitProps[3].vValue.vt = VT_BSTR;  
        aInitProps[3].vValue.bstrVal = SysAllocString(L"SSPI");  
    } //end if  
  
    // Now that properties are set, construct the PropertySet array.  
    aInitPropSets[0].guidPropertySet = DBPROPSET_DBINIT;  
    aInitPropSets[0].cProperties = nProps;  
    aInitPropSets[0].rgProperties = aInitProps;  
  
    // Set initialization properties  
    pIDBInitialize->QueryInterface(IID_IDBProperties,  
        (void**) &pIDBProperties);  
    hr = pIDBProperties->SetProperties(nPropSets, aInitPropSets);  
    if (FAILED(hr))  
        {  
        // Display error from failed SetProperties.  
        }  
    pIDBProperties->Release();  
  
    // Free references on OLE known strings.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        if (aInitProps[nProp].vValue.vt == VT_BSTR)  
            SysFreeString(aInitProps[nProp].vValue.bstrVal);  
        }  
  
    for (nProp = 0; nProp < nSSProps; nProp++)  
        {  
        if (aSSInitProps[nProp].vValue.vt == VT_BSTR)  
            SysFreeString(aSSInitProps[nProp].vValue.bstrVal);  
        }  
  
    // Free dynamically allocated memory.  
    delete [] aInitPropSets;  
    delete [] aSSInitProps;  
  
    // On success, persist the data source.  
    if (SUCCEEDED(hr))  
        {  
        pIDBInitialize->QueryInterface(IID_IPersistFile,  
            (void**) &pIPersistFile);  
  
        hr = pIPersistFile->Save(OLESTR("MyDataSource.txt"), FALSE);  
  
        if (FAILED(hr))  
            {  
            // Display errors from IPersistFile interface.  
            }  
        pIPersistFile->Release();  
        }  
  
    return (hr);  
    }  
```  
  
 <span data-ttu-id="82f3a-108">**B. 使用保存的資料來源初始化：**</span><span class="sxs-lookup"><span data-stu-id="82f3a-108">**B. Use persisted data source initialization:**</span></span>  
  
 <span data-ttu-id="82f3a-109">此範例會搭配其他初始化屬性來使用保存的資料來源物件，這些屬性會提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。</span><span class="sxs-lookup"><span data-stu-id="82f3a-109">This example uses a persisted data source object with additional initialization properties that provide a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login and password.</span></span>  
  
```  
HRESULT InitFromPersistedDS  
    (  
    IDBInitialize* pIDBInitialize,  
    WCHAR* pPersistedDSN,  
    WCHAR* pUID,  
    WCHAR* pPWD  
    )  
    {  
    //const ULONG   nProps = 3;  
    const ULONG     nProps = 1;  
    const ULONG     nPropSets = 1;  
    ULONG           nProp;  
    IDBProperties*  pIDBProperties  = NULL;  
    IPersistFile*   pIPersistFile   = NULL;  
    DBPROP          aInitProps[nProps];  
    DBPROPSET       aInitPropSets[nPropSets];  
    HRESULT         hr;  
  
    // First load the persisted data source information.  
    pIDBInitialize->QueryInterface(IID_IPersistFile,  
        (void**) &pIPersistFile);  
  
    hr = pIPersistFile->Load(pPersistedDSN, STGM_DIRECT);  
  
    if (FAILED(hr))  
        {  
        // Display errors from IPersistFile interface.  
        }  
    pIPersistFile->Release();  
  
    if (FAILED(hr))  
        {  
        return (hr);  
        }  
  
    // Initialize common property options.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        VariantInit(&aInitProps[nProp].vValue);  
        aInitProps[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        aInitProps[nProp].colid = DB_NULLID;  
        }  
  
    // Level of prompting that will be done to complete the connection  
    // process.  
    aInitProps[0].dwPropertyID = DBPROP_INIT_PROMPT;  
    aInitProps[0].vValue.vt = VT_I2;  
    aInitProps[0].vValue.iVal = DBPROMPT_NOPROMPT;      
  
    // Now that properties are set, construct the PropertySet array.  
    aInitPropSets[0].guidPropertySet = DBPROPSET_DBINIT;  
    aInitPropSets[0].cProperties = nProps;  
    aInitPropSets[0].rgProperties = aInitProps;  
  
    // Set initialization properties  
    pIDBInitialize->QueryInterface(IID_IDBProperties,  
        (void**) &pIDBProperties);  
    hr = pIDBProperties->SetProperties(nPropSets, aInitPropSets);  
    if (SUCCEEDED(hr))  
        {  
        hr = pIDBInitialize->Initialize();  
        if (FAILED(hr))  
            {  
            DumpError(pIDBInitialize, IID_IDBInitialize);  
            }  
        }  
    else  
        {  
        // Display error from failed SetProperties.  
        }  
    pIDBProperties->Release();  
  
    // Free references on OLE known strings.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        if (aInitProps[nProp].vValue.vt == VT_BSTR)  
            SysFreeString(aInitProps[nProp].vValue.bstrVal);  
        }  
  
    return (hr);  
    }  
```  
  
 <span data-ttu-id="82f3a-110">**IPersistFile::Save** 方法可以在呼叫 **IDBInitialize::Initialize** 之前或之後呼叫。</span><span class="sxs-lookup"><span data-stu-id="82f3a-110">The **IPersistFile::Save** method can be called before or after calling **IDBInitialize::Initialize**.</span></span> <span data-ttu-id="82f3a-111">當從 **IDBInitialize::Initialize** 成功傳回之後呼叫此方法時，可確保已保存有效的資料來源規格。</span><span class="sxs-lookup"><span data-stu-id="82f3a-111">Calling the method after a successful return from **IDBInitialize::Initialize** ensures a valid data source specification is persisted.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="82f3a-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="82f3a-112">See Also</span></span>  
 [<span data-ttu-id="82f3a-113">資料來源物件 &#40;OLE DB&#41;</span><span class="sxs-lookup"><span data-stu-id="82f3a-113">Data Source Objects &#40;OLE DB&#41;</span></span>](data-source-objects-ole-db.md)  
  
  
