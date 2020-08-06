---
title: 自訂工作流程 XML 描述 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 77906426ddb901ec422367bf30aabef2e532ad06
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607427"
---
# <a name="custom-workflow-xml-description-master-data-services"></a>自訂工作流程 XML 描述 (Master Data Services)
  在中 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ，當工作流程啟動時，SQL SERVER MDS 工作流程整合服務會呼叫[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130))方法。 此方法會收到有關觸發工作流程商務規則之項目的中繼資料和資料，做為 XML 的區塊。 如需實作工作流程處理常式的範例程式碼，請參閱[自訂工作流程範例 &#40;Master Data Services&#41;](create-a-custom-workflow-example.md)。  
  
 以下範例顯示傳送至工作流程處理常式之 XML 的可能外觀：  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 下表描述此 XML 中包含的某些標記：  
  
|Tag|描述|  
|---------|-----------------|  
|\<Type>|您在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 之 [工作流程類型]**** 文字方塊中輸入的文字，用以識別要載入的自訂工作流程組件。|  
|\<SendData>|在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中，由 [訊息中包含成員資料]**** 核取方塊所控制的布林值。 值為1表示 \<MemberData> 會傳送區段，否則 \<MemberData> 不會傳送區段。|  
|<Server_URL>|您在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 之 [工作流程網站]**** 文字方塊中輸入的文字。|  
|<Action_ID>|您在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 之 [工作流程名稱]**** 文字方塊中輸入的文字。|  
|\<MemberData>|包含觸發工作流程動作之成員的資料。 只有在的值為1時，才會包含此項 \<SendData> 。|  
|\<Enter*xxx*>|這組標記包含有關建立成員的中繼資料，例如建立成員的時間以及建立成員者。|  
|\<LastChg*xxx*>|這組標記包含有關上次對成員所進行之變更的中繼資料，例如進行變更的時間以及進行變更者。|  
|\<Name>|已變更之成員的第一個屬性。 此範例成員僅包含 Name 和 Code 屬性。|  
|\<Code>|已變更之成員的下一個屬性。 如果此範例成員包含更多屬性，則會緊接著此屬性之後。|  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂工作流程 &#40;Master Data Services&#41;](create-a-custom-workflow-master-data-services.md)   
 [自訂工作流程範例 &#40;Master Data Services&#41;](create-a-custom-workflow-example.md)  
  
  
