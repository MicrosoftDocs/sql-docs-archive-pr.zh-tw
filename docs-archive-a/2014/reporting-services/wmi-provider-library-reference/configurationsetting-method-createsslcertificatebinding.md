---
title: CreateSSLCertificateBinding 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- CreateSSLCertificateBinding
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8b9a5f9394d655f7b0592ea688a46f3ac2b9c153
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594931"
---
# <a name="createsslcertificatebinding-method-wmi-msreportserver_configurationsetting"></a>CreateSSLCertificateBinding 方法 (WMI MSReportServer_ConfigurationSetting)
  建立 SSL 憑證繫結。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *應用程式*  
 應該建立憑證繫結之應用程式的名稱。  
  
 *CertificateHash*  
 憑證的雜湊。  
  
 *IPAddress*  
 應用程式的 IP 位址。  
  
 *通訊埠*  
 與繫結相關聯的 SSL 通訊埠。  
  
 *Lcid*  
 要用於傳回之錯誤訊息的地區設定。  
  
 *錯誤*  
 [out] 發生之錯誤的描述。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。錯誤碼則表示呼叫不成功。  
  
## <a name="remarks"></a>備註  
 這個方法會加入應用程式之 rsreportserver.config 的繫結。 如果繫結尚未存在 HTTP.SYS 中，就會在該處建立繫結。  
  
 建立繫結之前，此方法呼叫會檢查指定之應用程式的 URL 保留項目，以便判斷 SSL 憑證繫結是否有效。  
  
 下列條件會進行驗證而且可能會產生錯誤：  
  
1.  憑證不存在。  
  
2.  指定的 IPAddress 並未對應至這部電腦的 IPAddress。  
  
3.  指定的 IPAddress 是 DHCP IPAddress (定期變更) - 請改用萬用字元 IP 位址 (0.0.0.0)。  
  
4.  指定的 IPAddress 與 URL 保留項目的 IP 位址不符，而且萬用字元或主機名稱 URL 保留項目不存在。  
  
5.  指定主機名稱的 URL 保留項目存在，但是此主機名稱與憑證主機名稱不符。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
