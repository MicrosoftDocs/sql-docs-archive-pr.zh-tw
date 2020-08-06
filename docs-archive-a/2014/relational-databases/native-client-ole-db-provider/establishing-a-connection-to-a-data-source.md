---
title: 建立與資料來源的連線 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [SQL Server Native Client]
- connections [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, data source connections
- CoCreateInstance method
- OLE DB data sources [SQL Server Native Client]
ms.assetid: 7ebd1394-cc8d-4bcf-92f3-c374a26e7ba0
author: rothja
ms.author: jroth
ms.openlocfilehash: f88454339ee932c38655819cce475ab52d79975f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598836"
---
# <a name="establishing-a-connection-to-a-data-source"></a><span data-ttu-id="1e0d8-102">建立資料來源的連接</span><span class="sxs-lookup"><span data-stu-id="1e0d8-102">Establishing a Connection to a Data Source</span></span>
  <span data-ttu-id="1e0d8-103">若要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，取用者必須先呼叫**CoCreateInstance**方法來建立資料來源物件的實例。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-103">To access the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider, the consumer must first create an instance of a data source object by calling the **CoCreateInstance** method.</span></span> <span data-ttu-id="1e0d8-104">唯一類別識別項 (CLSID) 會識別每個 OLE DB 提供者。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-104">A unique class identifier (CLSID) identifies each OLE DB provider.</span></span> <span data-ttu-id="1e0d8-105">針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，類別識別碼為 CLSID_SQLNCLI10。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-105">For the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider, the class identifier is CLSID_SQLNCLI10.</span></span> <span data-ttu-id="1e0d8-106">您也可以使用符號 SQLNCLI_CLSID，解析為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您所參考的 SQLNCLI 中所使用的 Native Client OLE DB 提供者。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-106">You can also use the symbol SQLNCLI_CLSID that will resolve to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider that is used in the sqlncli.h that you reference.</span></span>  
  
 <span data-ttu-id="1e0d8-107">資料來源物件會公開 **IDBProperties** 介面，取用者可以使用這個介面來提供基本驗證資訊；例如，伺服器名稱、資料庫名稱、使用者識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-107">The data source object exposes the **IDBProperties** interface, which the consumer uses to provide basic authentication information such as server name, database name, user ID, and password.</span></span> <span data-ttu-id="1e0d8-108">呼叫 **IDBProperties::SetProperties** 方法可設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-108">The **IDBProperties::SetProperties** method is called to set these properties.</span></span>  
  
 <span data-ttu-id="1e0d8-109">如果有多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體在電腦上執行，伺服器名稱會指定為 ServerName\InstanceName。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-109">If there are multiple instances of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] running on the computer, the server name is specified as ServerName\InstanceName.</span></span>  
  
 <span data-ttu-id="1e0d8-110">資料來源物件也會公開 **IDBInitialize** 介面。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-110">The data source object also exposes the **IDBInitialize** interface.</span></span> <span data-ttu-id="1e0d8-111">屬性設定之後，就會呼叫 **IDBInitialize::Initialize** 方法來建立資料來源的連線。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-111">After the properties are set, connection to the data source is established by calling the **IDBInitialize::Initialize** method.</span></span> <span data-ttu-id="1e0d8-112">例如：</span><span class="sxs-lookup"><span data-stu-id="1e0d8-112">For example:</span></span>  
  
```  
CoCreateInstance(CLSID_SQLNCLI10,   
                 NULL,   
                 CLSCTX_INPROC_SERVER,  
                 IID_IDBInitialize,   
                 (void **) &pIDBInitialize)  
```  
  
 <span data-ttu-id="1e0d8-113">這個對**CoCreateInstance**的呼叫會建立與 CLSID_SQLNCLI10 相關聯之類別的單一物件，而與用來建立物件) 的資料和程式碼關聯的 (CSLID。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-113">This call to **CoCreateInstance** creates a single object of the class associated with CLSID_SQLNCLI10 (CSLID associated with the data and code that will be used to create the object).</span></span> <span data-ttu-id="1e0d8-114">IID_IDBInitialize 是介面 (**IDBInitialize**) 識別項的參考，用於與物件進行通訊。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-114">IID_IDBInitialize is a reference to the identifier of the interface (**IDBInitialize**) to be used to communicate with the object.</span></span>  
  
 <span data-ttu-id="1e0d8-115">以下是初始化與建立資料來源之連接的範例函數。</span><span class="sxs-lookup"><span data-stu-id="1e0d8-115">The following is a sample function that initializes and establishes a connection to the data source.</span></span>  
  
```  
void InitializeAndEstablishConnection() {  
   // Initialize the COM library.  
   CoInitialize(NULL);  
  
   // Obtain access to the SQL Server Native Client OLE DB provider.  
   hr = CoCreateInstance(CLSID_SQLNCLI10,   
                         NULL,   
                         CLSCTX_INPROC_SERVER,  
                         IID_IDBInitialize,   
                         (void **) &pIDBInitialize);  
   // Initialize property values needed to establish connection.  
   for (i = 0 ; i < 4 ; i++)   
      VariantInit(&InitProperties[i].vValue);  
  
   // Server name.  
   // See DBPROP structure for more information on InitProperties  
   InitProperties[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
   InitProperties[0].vValue.vt    = VT_BSTR;  
   InitProperties[0].vValue.bstrVal=   
                     SysAllocString(L"Server");  
   InitProperties[0].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[0].colid       = DB_NULLID;  
  
   // Database.  
   InitProperties[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
   InitProperties[1].vValue.vt    = VT_BSTR;  
   InitProperties[1].vValue.bstrVal= SysAllocString(L"database");  
   InitProperties[1].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[1].colid       = DB_NULLID;  
  
   // Username (login).  
   InitProperties[2].dwPropertyID  = DBPROP_AUTH_INTEGRATED;  
   InitProperties[2].vValue.vt    = VT_BSTR;  
   InitProperties[2].vValue.bstrVal= SysAllocString(L"SSPI");  
   InitProperties[2].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[2].colid       = DB_NULLID;  
   InitProperties[3].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[3].colid       = DB_NULLID;  
  
   // Construct the DBPROPSET structure(rgInitPropSet). The   
   // DBPROPSET structure is used to pass an array of DBPROP   
   // structures (InitProperties) to the SetProperties method.  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties   = 4;  
   rgInitPropSet[0].rgProperties   = InitProperties;  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                           (void **)&pIDBProperties);  
   hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
   pIDBProperties->Release();  
  
   // Now establish the connection to the data source.  
   pIDBInitialize->Initialize();  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="1e0d8-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1e0d8-116">See Also</span></span>  
 [<span data-ttu-id="1e0d8-117">建立 SQL Server Native Client OLE DB 提供者應用程式</span><span class="sxs-lookup"><span data-stu-id="1e0d8-117">Creating a SQL Server Native Client OLE DB Provider Application</span></span>](creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
