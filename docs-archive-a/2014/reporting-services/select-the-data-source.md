---
title: 選取資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.selectdatasource.f1
ms.assetid: cdd84ad8-7c6a-41ac-bf51-1b0973434829
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 641aa04f7fe658123aa21cc1bd21264ec0ee28ea
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688477"
---
# <a name="select-the-data-source"></a>選取資料來源
  使用報表精靈的這個頁面，即可定義報表的資料來源。  
  
## <a name="options"></a>選項  
 **共用資料來源**  
 選取 [共用資料來源]****，即可使用預先定義的共用資料來源，且其已擁有您想要使用的資料來源連接資訊。 此清單包含專案中所包含的所有共用資料來源。  
  
 **新增資料來源**  
 選取 [新增資料來源]****，即可定義新的資料來源。 資料來源資訊只會用於目前的報表。  
  
 **名稱**  
 輸入資料來源之連接的名稱。 資料來源名稱在報表內必須是唯一的。  
  
 **型別**  
 選取您要使用的資料來源類型 (例如，如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫，請選擇 [) ] [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
 **連接字串**  
 輸入資料來源的連接字串。 如需連接字串的詳細資訊，請參閱[Reporting Services 中的資料連線、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
 按一下 **[編輯]** ，即可在 **[連接屬性]** 對話方塊中指定資料來源伺服器。 您可以指定本機或遠端資料來源。  
  
 按一下 **[認證]** ，即可提供資料庫認證。 至少您指定的認證必須足以讓您基於報表設計用途，來連接到資料來源。 當報表是部署在報表伺服器上時，資料庫認證必須配合報表的所有使用者。 例如，如果您希望所有報表使用者都使用其認證來連接到資料來源，請選擇 [使用 Windows 驗證 (整合式安全性)]****。 您指定的認證對於資料來源必須是有效的，所以如果您選擇 Windows 驗證，請確定資料來源會接受來自將執行報表之所有使用者帳戶的連接。 資料庫認證可以從報表中個別加以管理。 如需詳細資訊，請參閱 [管理報表資料來源](report-data/manage-report-data-sources.md)。  
  
 **將此做為共用資料來源**  
 選取此選項，即可將資料來源儲存在專案中當做共用資料來源，而不是儲存在報表中。 如此一來，您就可以將它當做專案中其他報表的資料來源使用。  
  
## <a name="see-also"></a>另請參閱  
 [內嵌和共用資料連線或資料來源 &#40;報表產生器和 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [指定報表資料來源的認證及連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Reporting Services 報表伺服器](../../2014/reporting-services/reporting-services-report-server.md)   
 [Rsreportdesigner.config 設定檔](report-server/rsreportdesigner-configuration-file.md)   
 [Reporting Services 中的資料連線、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [報表精靈說明](../../2014/reporting-services/report-wizard-help.md)  
  
  
