---
title: 設定大型資料 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- large data
ms.assetid: b057f04b-e5f4-466e-a39a-090dae797236
author: rothja
ms.author: jroth
ms.openlocfilehash: cd88a31867c1a6cebafa9ec15011562286ae336d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597097"
---
# <a name="set-large-data-ole-db"></a>設定大型資料 (OLE DB)
  此範例會示範如何設定 BLOB 資料、建立資料表、加入範例記錄、在資料列集中提取該記錄，然後設定 BLOB 欄位的值。 IA64 不支援此範例。  
  
 若要傳遞自己的儲存物件指標，取用者會建立一個繫結 BLOB 資料行值的存取子，然後呼叫 `IRowsetChange::SetData` 或 `IRowsetChange::InsertRow` 方法。  
  
 此範例需要 AdventureWorks 範例資料庫，您可以從 [Microsoft SQL Server Samples and Community Projects](https://go.microsoft.com/fwlink/?LinkID=85384) (Microsoft SQL Server 範例和社群專案首頁) 下載。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。 如果無法使用 Windows 驗證，請提示使用者在執行階段輸入認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，您應該使用[Win32 加密 API](https://go.microsoft.com/fwlink/?LinkId=64532)將它們加密。  
  
## <a name="procedures"></a>程序  
  
#### <a name="to-set-blob-data"></a>設定 BLOB 資料  
  
1.  建立一個 DBOBJECT 結構，描述如何存取 BLOB 資料行。 將 DBOBJECT 結構的**dwFlag**元素設定為 STGM_READ，並將 iid 元素設定為 `IID_ISequentialStream` (要公開) 的介面。  
  
2.  在 DBPROPSET_ROWSET 屬性群組中設定屬性，讓資料列集可以更新。  
  
3.  使用 DBBINDING 結構的陣列來建立一組繫結 (每個資料行一個)。 將 DBBINDING 結構中的 **wType** 項目設定為 DBTYPE_IUNKNOWN，並將 **pObject** 項目設定為指向您所建立的 DBOBJECT 結構。  
  
4.  使用繫結資訊，在結構的 DBBINDINGS 陣列中建立存取子。  
  
5.  呼叫 `GetNextRows` 將下一個資料列提取到資料列集中。 呼叫 `GetData` 來讀取資料列集中的資料。  
  
6.  若要設定資料，建立包含資料 (以及長度指標) 的儲存物件，然後使用繫結 BLOB 資料行的存取子，呼叫 `IRowsetChange::SetData` (或 `IRowsetChange::InsertRow`)。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 使用 ole32.lib oleaut32.lib 編譯並執行下列 C++ 程式碼清單。 這個應用程式會連接到電腦的預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 在某些 Windows 作業系統上，您必須將 (localhost) 或 (local) 變更為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。 若要連線到具名執行個體，請將連接字串從 L"(local)" 變更為 L"(local)\\\name"，其中 name 是具名執行個體。 根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 會安裝至具名執行個體。 請確認您的 INCLUDE 環境變數包含的目錄內含 sqlncli.h。  
  
### <a name="code"></a>程式碼  
  
```  
// compile with: ole32.lib oleaut32.lib  
#define UNICODE  
#define DBINITCONSTANTS  
#define INITGID  
#define OLEDBVER 0x0250  // to include correct interfaces  
  
#include <windows.h>  
#include <stdio.h>  
#include <stddef.h>  
#include <iostream>  
#include <oledb.h>  
#include <oledberr.h>  
#include <SQLNCLI.h>  
  
using namespace std;  
  
#define SAFE_RELEASE(pIUnknown) if(pIUnknown) (pIUnknown)->Release();  
HRESULT GetCommandObject(REFIID riid, IUnknown** ppIUnknown);  
HRESULT CreateTable(ICommandText* pICommandText);  
  
class CSeqStream : public ISequentialStream {  
public:  
   // Constructors  
   CSeqStream();  
   virtual ~CSeqStream();  
  
   virtual BOOL Seek(ULONG iPos);  
   virtual BOOL Clear();  
   virtual BOOL CompareData(void* pBuffer);  
   virtual ULONG Length() { return m_cBufSize; };  
  
   virtual operator void* const() { return m_pBuffer; };  
  
   STDMETHODIMP_(ULONG) AddRef(void);  
   STDMETHODIMP_(ULONG) Release(void);  
   STDMETHODIMP QueryInterface(REFIID riid, LPVOID *ppv);  
  
   STDMETHODIMP Read(   
      /* [out] */ void __RPC_FAR *pv,  
      /* [in]  */ ULONG cb,  
      /* [out] */ ULONG __RPC_FAR *pcbRead);  
  
   STDMETHODIMP Write(   
      /* [in] */ const void __RPC_FAR *pv,  
      /* [in] */ ULONG cb,  
      /* [out]*/ ULONG __RPC_FAR *pcbWritten);  
  
private:  
   ULONG m_cRef;   // reference count  
   void* m_pBuffer;   // buffer  
   ULONG m_cBufSize;   // buffer size  
   ULONG m_iPos;   // current index position in the buffer  
};  
  
// class implementation  
CSeqStream::CSeqStream() {  
   m_iPos = 0;  
   m_cRef = 0;  
   m_pBuffer = NULL;  
   m_cBufSize = 0;  
  
   // The constructor AddRef's  
   AddRef();  
}  
  
CSeqStream::~CSeqStream() {  
   // Shouldn't have any references left ASSERT(m_cRef == 0);  
   CoTaskMemFree(m_pBuffer);  
}  
  
ULONG CSeqStream::AddRef() {  
   return ++m_cRef;  
}  
  
ULONG CSeqStream::Release() {  
   // ASSERT(m_cRef);  
   if (--m_cRef)  
      return m_cRef;  
  
   delete this;  
   return 0;  
}  
  
HRESULT CSeqStream::QueryInterface(REFIID riid, void** ppv) {  
   // ASSERT(ppv);  
   *ppv = NULL;  
  
   if (riid == IID_IUnknown)  
      *ppv = this;  
  
   if (riid == IID_ISequentialStream)  
      *ppv = this;  
  
   if(*ppv) {  
      ((IUnknown*)*ppv)->AddRef();  
      return S_OK;  
   }  
  
   return E_NOINTERFACE;  
}  
  
BOOL CSeqStream::Seek(ULONG iPos) {  
   // Make sure the desired position is within the buffer  
   // ASSERT(iPos == 0 || iPos < m_cBufSize);  
  
   // Reset the current buffer position  
   m_iPos = iPos;  
   return TRUE;  
}  
  
BOOL CSeqStream::Clear() {  
   // Frees the buffer  
   m_iPos = 0;  
   m_cBufSize = 0;  
  
   CoTaskMemFree(m_pBuffer);  
   m_pBuffer = NULL;  
  
   return TRUE;  
}  
  
BOOL CSeqStream::CompareData(void* pBuffer) {  
   // ASSERT(pBuffer);  
  
   // Quick and easy way to compare user buffer with the stream  
   return memcmp(pBuffer, m_pBuffer, m_cBufSize) == 0;  
}  
  
HRESULT CSeqStream::Read(void *pv, ULONG cb, ULONG* pcbRead) {  
   // Parameter checking  
   if (pcbRead)  
      *pcbRead = 0;  
  
   if (!pv)  
      return STG_E_INVALIDPOINTER;  
  
   if (cb == 0)  
      return S_OK;  
  
   // Actual code  
   ULONG cBytesLeft = m_cBufSize - m_iPos;  
   ULONG cBytesRead = cb > cBytesLeft ? cBytesLeft : cb;  
  
   // if no more bytes to retrieve return   
   if (cBytesLeft == 0)  
      return S_FALSE;   
  
   // Copy to users buffer the number of bytes requested or remaining  
   memcpy(pv, (void*)((BYTE*)m_pBuffer + m_iPos), cBytesRead);  
   m_iPos += cBytesRead;  
  
   if (pcbRead)  
      *pcbRead = cBytesRead;  
  
   if (cb != cBytesRead)  
      return S_FALSE;   
  
   return S_OK;  
}  
  
HRESULT CSeqStream::Write(const void *pv, ULONG cb, ULONG* pcbWritten) {  
   // Parameter checking  
   if (!pv)  
      return STG_E_INVALIDPOINTER;  
  
   if (pcbWritten)  
      *pcbWritten = 0;  
  
   if (cb == 0)  
      return S_OK;  
  
   // Enlarge the current buffer  
   m_cBufSize += cb;  
  
   // Need to append to the end of the stream  
   m_pBuffer = CoTaskMemRealloc(m_pBuffer, m_cBufSize);  
   memcpy((void*)((BYTE*)m_pBuffer + m_iPos), pv, cb);  
   // m_iPos += cb;  
  
   if (pcbWritten)  
      *pcbWritten = cb;  
  
   return S_OK;  
}  
  
int main() {  
   CoInitialize(NULL);  
  
   DBOBJECT ObjectStruct;  
   ObjectStruct.dwFlags = STGM_READ;  
   ObjectStruct.iid = IID_ISequentialStream;  
  
   struct BLOBDATA {  
      DBSTATUS dwStatus;     
      DBLENGTH dwLength;   
      ISequentialStream* pISeqStream;  
   };  
  
   BLOBDATA BLOBGetData;  
   BLOBDATA BLOBSetData;  
  
   const ULONG cBindings = 1;  
   DBBINDING rgBindings[cBindings];   
   HRESULT hr = S_OK;  
  
   IAccessor* pIAccessor = NULL;  
   ICommandText* pICommandText = NULL;  
   ICommandProperties* pICommandProperties = NULL;  
   IRowsetChange* pIRowsetChange = NULL;  
   IRowset* pIRowset = NULL;  
   CSeqStream* pMySeqStream = NULL;  
  
   DBCOUNTITEM cRowsObtained = 0;  
   HACCESSOR hAccessor = DB_NULL_HACCESSOR;  
   DBBINDSTATUS rgBindStatus[cBindings];  
   HROW* rghRows = NULL;  
  
   const ULONG cPropSets = 1;  
   DBPROPSET rgPropSets[cPropSets];  
   const ULONG cProperties = 1;  
   DBPROP rgProperties[cProperties];  
   const ULONG cBytes = 10;  
  
   BYTE pBuffer[cBytes];  
   ULONG cBytesRead = 0;  
  
   BYTE pReadData[cBytes];   // read BLOB data in this array  
   memset(pReadData, 0xAA, cBytes);  
  
   BYTE pWriteData[cBytes];   // write BLOB data from this array  
   memset(pWriteData, 'D', cBytes);  
  
   // Get Command object  
   hr = GetCommandObject(IID_ICommandText, (IUnknown**)&pICommandText);  
   if (FAILED(hr)) {  
      printf("Failed to get ICommandText interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Create table with image column and index  
   hr = CreateTable(pICommandText);  
   if (FAILED(hr)) {  
      printf("Failed to create table.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Set the DBPROPSET structure.  It is used to pass an array   
   // of DBPROP structures to SetProperties().  
   rgPropSets[0].guidPropertySet = DBPROPSET_ROWSET;  
   rgPropSets[0].cProperties = cProperties;  
   rgPropSets[0].rgProperties = rgProperties;  
  
   // Now set properties in the property group (DBPROPSET_ROWSET)  
   rgPropSets[0].rgProperties[0].dwPropertyID = DBPROP_UPDATABILITY;  
   rgPropSets[0].rgProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgPropSets[0].rgProperties[0].dwStatus = DBPROPSTATUS_OK;  
   rgPropSets[0].rgProperties[0].colid = DB_NULLID;  
   rgPropSets[0].rgProperties[0].vValue.vt = VT_I4;  
   V_I4(&rgPropSets[0].rgProperties[0].vValue) = DBPROPVAL_UP_CHANGE;  
  
   // Set the rowset properties  
   hr = pICommandText->QueryInterface(IID_ICommandProperties,  
      (void **)&pICommandProperties);  
  
   if (FAILED(hr)) {  
      printf("Failed to get ICommandProperties to set rowset properties.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandProperties->SetProperties(cPropSets, rgPropSets);  
  
   if (FAILED(hr)) {  
      printf("Execute failed to set rowset properties.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Execute a command (SELECT * FROM TestISeqStream)  
   hr = pICommandText->SetCommandText(DBGUID_DBSQL, L"SELECT * FROM TestISeqStream");  
  
   if (FAILED(hr)) {  
      printf("Failed to set command text SELECT * FROM.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandText->Execute(NULL,   
      IID_IRowsetChange,   
      NULL,   
      NULL,  
      (IUnknown**)&pIRowsetChange);  
  
   if (FAILED(hr)) {  
      printf("Failed to execute the command SELECT * FROM.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Fill the DBBINDINGS array.  
   rgBindings[0].iOrdinal = 2;   // ordinal position  
   rgBindings[0].obValue = offsetof(BLOBDATA, pISeqStream);  
   rgBindings[0].obLength = offsetof(BLOBDATA, dwLength);  
   rgBindings[0].obStatus = offsetof(BLOBDATA, dwStatus);  
   rgBindings[0].pTypeInfo = NULL;  
   rgBindings[0].pObject = &ObjectStruct;  
   rgBindings[0].pBindExt = NULL;  
   rgBindings[0].dwPart =  DBPART_VALUE | DBPART_STATUS | DBPART_LENGTH;  
   rgBindings[0].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
   rgBindings[0].eParamIO = DBPARAMIO_NOTPARAM;  
   rgBindings[0].cbMaxLen = 0;   
   rgBindings[0].dwFlags = 0;  
   rgBindings[0].wType = DBTYPE_IUNKNOWN;  
   rgBindings[0].bPrecision = 0;  
   rgBindings[0].bScale = 0;  
  
   // Create an accessor using the binding information.  
   hr = pIRowsetChange->QueryInterface(IID_IAccessor, (void**)&pIAccessor);  
   if (FAILED(hr)) {  
      printf("Failed to get IAccessor interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA,  
      cBindings,  
      rgBindings,   
      sizeof(BLOBDATA),  
      &hAccessor,  
      rgBindStatus);  
  
   if (FAILED(hr)) {  
      printf("Failed to create an accessor.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // get the first row.  
   hr = pIRowsetChange->QueryInterface(IID_IRowset, (void **)&pIRowset);  
   if (FAILED(hr)) {  
      printf("Failed to get IRowset interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIRowset->GetNextRows(NULL, 0, 1, &cRowsObtained, &rghRows);  
   hr = pIRowset->GetData(rghRows[0], hAccessor, &BLOBGetData);  
  
   // Verify the retrieved data, only if data is not null.  
   if (BLOBGetData.dwStatus == DBSTATUS_S_ISNULL) {  
      // Process null data  
      printf("Provider returned a null value.\n");  
   }   
   else if(BLOBGetData.dwStatus == DBSTATUS_S_OK) {  
      // Provider returned a nonNULL value  
      BLOBGetData.pISeqStream->Read( pBuffer, cBytes, &cBytesRead);  
  
      if (memcmp(pBuffer, pReadData, cBytes) != 0) {  
         // cleanup   
      }  
  
      SAFE_RELEASE(BLOBGetData.pISeqStream);  
   }  
  
   // Set up data for SetData.  
   pMySeqStream = new CSeqStream();  
  
   // Put data into ISequentialStream object for the provider to write.  
   pMySeqStream->Write(pWriteData, cBytes, NULL);  
  
   BLOBSetData.pISeqStream = (ISequentialStream*)pMySeqStream;  
   BLOBSetData.dwStatus = DBSTATUS_S_OK;  
   BLOBSetData.dwLength = pMySeqStream->Length();  
  
   // Set the data.  
   hr = pIRowsetChange->SetData(rghRows[0], hAccessor, &BLOBSetData);  
   if (FAILED(hr))     {  
      printf("Failed to set data.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIAccessor->ReleaseAccessor(hAccessor, NULL);  
   if (FAILED(hr)) {  
      printf("Failed to release accessor.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIRowset->ReleaseRows(cRowsObtained, rghRows, NULL, NULL, NULL);  
  
   if (FAILED(hr)) {  
      printf("Failed to release rows.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
Exit:  
   // Release all allocated memory and release interface pointers.  
   CoUninitialize();  
}  
  
HRESULT GetCommandObject(REFIID riid, IUnknown** ppIUnknown) {  
   HRESULT hr = S_OK;  
  
   // Local interface pointers, until a connection is made.  
   IDBInitialize* pIDBInitialize = NULL;  
   IDBProperties*  pIDBProperties = NULL;  
   IDBCreateSession* pIDBCreateSession = NULL;  
   IDBCreateCommand* pIDBCreateCommand = NULL;  
  
   const ULONG cPropSets = 1;  
   DBPROPSET rgPropSets[cPropSets];  
  
   const ULONG cProperties = 4;  
   DBPROP rgProperties[cProperties];  
  
   // Initialize property values needed to establish connection.  
   for ( ULONG i = 0 ; i < 4 ; i++ )  
      VariantInit(&rgProperties[i].vValue);  
  
   // Server name.  
   rgProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   rgProperties[0].vValue.vt = VT_BSTR;  
  
   rgProperties[0].vValue.bstrVal = SysAllocString(L"(local)");  
   rgProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgProperties[0].colid = DB_NULLID;  
  
   // Database.  
   rgProperties[1].dwPropertyID = DBPROP_INIT_CATALOG;  
   rgProperties[1].vValue.vt = VT_BSTR;  
   rgProperties[1].vValue.bstrVal = SysAllocString(L"AdventureWorks");  
   rgProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgProperties[1].colid = DB_NULLID;  
  
   rgProperties[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;  
   rgProperties[2].vValue.vt = VT_BSTR;  
   rgProperties[2].vValue.bstrVal = SysAllocString(L"SSPI");  
   rgProperties[2].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgProperties[2].colid = DB_NULLID;  
  
   // Properties are now set.  Next, construct DBPROPSET structure (rgInitPropSet) used to pass an   
   // array of DBPROP structures (InitProperties) to the SetProperties method.  
   rgPropSets[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgPropSets[0].cProperties = cProperties;  
   rgPropSets[0].rgProperties = rgProperties;  
  
   // Get the IDBInitialize interface.  
   hr = CoCreateInstance(CLSID_SQLNCLI11,   
      NULL,   
      CLSCTX_INPROC_SERVER,  
      IID_IDBInitialize,   
      (void**)&pIDBInitialize);  
  
   if (FAILED(hr)) {  
      printf("Failed to get IDBInitialize interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);  
   if (FAILED(hr)) {  
      printf("Failed to get IDBProperties interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIDBProperties->SetProperties(cPropSets, rgPropSets);  
   if (FAILED(hr)) {  
      printf("Failed to set properties for DBPROPSET_DBINIT.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIDBInitialize->Initialize();  
   if (FAILED(hr)) {  
      printf("Failed to initialize.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Create a session object.  
   hr = pIDBInitialize->QueryInterface( IID_IDBCreateSession,  
                                        (void **)&pIDBCreateSession);  
  
   if (FAILED(hr)) {  
      printf("Failed to get pIDBCreateSession interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIDBCreateSession->CreateSession( NULL, IID_IDBCreateCommand, (IUnknown**)&pIDBCreateCommand);  
  
   if (FAILED(hr)) {  
      printf("Failed to create session object.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Get CommandText object  
   hr = pIDBCreateCommand->CreateCommand( NULL, riid, (IUnknown**)ppIUnknown);  
  
   if (FAILED(hr)) {  
      printf("Failed to create CommandText object.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   return hr;  
  
Exit:  
   // Free up all allocated memory and release interface pointers.  
   return hr;  
}  
  
HRESULT CreateTable(ICommandText* pICommandText) {  
   HRESULT hr = S_OK;  
  
   // drop the table "TestISeqStream" if the table exists.  
   hr = pICommandText->SetCommandText( DBGUID_DBSQL, L"if object_id('TestISeqStream') is not null drop table TestISeqStream");  
   if (FAILED(hr)) {  
      printf("Failed to set command text DROP TABLE.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandText->Execute(NULL, IID_NULL, NULL, NULL, NULL);  
   if (FAILED(hr)) {  
      printf("Failed to drop the table.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Create a new table.  
   hr = pICommandText->SetCommandText(DBGUID_DBSQL,   
      L"CREATE TABLE TestISeqStream (col1 int,col2 image)");  
  
   if (FAILED(hr)) {  
      printf("Failed to set command text CREATE TABLE.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandText->Execute(NULL, IID_NULL, NULL, NULL, NULL);  
   if (FAILED(hr)) {  
      printf("Failed to create table.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Insert one row into table.  
   hr = pICommandText->SetCommandText(DBGUID_DBSQL,  
      L"INSERT INTO TestISeqStream(col1,col2) VALUES (1,0xAAAAAAAAAAAAAAAAA)");  
   if (FAILED(hr)) {  
      printf("Failed to set command text INSERT INTO.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandText->Execute(NULL, IID_NULL, NULL, NULL, NULL);  
  
   if (FAILED(hr)) {  
      printf("Failed to insert record in the table.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
Exit:  
   // Release all allocated memory and release interface pointers.  
   return hr;  
}  
```  
  
  
