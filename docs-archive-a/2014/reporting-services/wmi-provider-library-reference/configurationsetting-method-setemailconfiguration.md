---
title: SetEmailConfiguration 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 19068d7d7fff8c31c455ef76e8d2c2caa26b743f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706062"
---
# <a name="setemailconfiguration-method-wmi-msreportserver_configurationsetting"></a>SetEmailConfiguration 方法 (WMI MSReportServer_ConfigurationSetting)
  設定報表伺服器用來傳送電子郵件的電子郵件傳遞延伸模組。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetEmailConfiguration(ByVal SendUsingSMTPServer As Boolean, _  
    ByVal SMTPServer As String, ByVal SenderEmailAddress As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetEmailConfiguration (Boolean SendUsingSMTPServer,   
   string SMTPServer, string SenderEmailAddress,   
   out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *SendUsingSMTPServer*  
 指出伺服器是否要使用 SMTP 伺服器來傳送電子郵件的布林值。 這個值只能設定為 true。 預設值為 false。  
  
 *SMTPServer*  
 包含 SMTP 伺服器之名稱或 IP 位址的字串。  
  
 *SenderEmailAddress*  
 在報表伺服器所傳送的電子郵件中，用於「寄件者:」欄位的電子郵件地址。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 當*SendUsingSMTPServer*參數設定為時 `true` ，報表伺服器設定檔中的**SendUsing**專案會設定為1。 當*SendUsingSMTPServer*設定為時 `false` ，未設定**SendUsing**專案。  
  
 這個方法無法讓使用者將報表伺服器組態檔中的 **SendUsing** 項目設定為 1 以外的值。 若要針對 SMTP 郵件以外的任何項目設定報表伺服器，您必須手動編輯此組態檔。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
