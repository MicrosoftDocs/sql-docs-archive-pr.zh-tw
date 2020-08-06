---
title: 建立、修改和刪除資料驅動訂閱 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0ec7fad729e5a7bd0f75d7a524ba315b4511a7a5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598732"
---
# <a name="create-modify-and-delete-a-data-driven-subscription"></a>Create, Modify, and Delete a Data-Driven Subscription
  資料驅動訂閱是查詢式訂閱，會在執行階段取得用於處理訂閱的資料值。 觸發訂閱時，會處理查詢以取得有關收件者、報表傳遞選項、轉譯格式，以及參數設定的最新資訊。 查詢結果會與訂閱定義結合，以建立動態訂閱，該動態訂閱會使用您已在員工資料庫、客戶資料庫，或包含可做為訂閱者資料之資訊的其他任何資料庫中維護的資料。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 &#124; SharePoint 模式|  
  
 **本主題內容：**  
  
-   [建立和修改資料驅動訂閱](#bkmk_create_and_modify)  
  
-   [定義查詢以擷取訂閱資訊](#bkmk_define_query)  
  
-   [執行訂閱](#bkmk_run_subscription)  
  
-   [管理和刪除資料驅動訂閱](#bkmk_manage_and_delete)  
  
##  <a name="create-and-modify-a-data-driven-subscription"></a><a name="bkmk_create_and_modify"></a>建立和修改資料驅動訂閱  
 若要建立新的資料驅動訂閱或修改現有的訂閱，請使用報表管理員中的 [建立資料驅動訂閱] 頁面。 這些頁面會引導您逐步建立或修改訂閱。 若要在訂閱建立之後存取，請使用 [我的訂閱] 頁面和報表的 [訂閱] 清單。 若要了解如何建立資料驅動訂閱，請參閱[建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)。  
  
 若要建立資料驅動訂閱，請選取使用預存認證或無認證的報表。 當您建立資料驅動訂閱時，請考慮使用 [描述] 欄位的命名慣例，如此就能輕鬆區分標準訂閱與資料驅動訂閱。  
  
#### <a name="to-create-a-data-driven-subscription-native-mode"></a>若要建立資料驅動訂閱 (原生模式)  
  
1.  在報表管理員中，導覽到包含報表的資料夾，將滑鼠停留在報表上方，接著開啟 [選項] 功能表，然後按一下 **[管理]**。  
  
2.  按一下 **[訂閱]** 索引標籤。  
  
3.  按一下 **[新增資料驅動訂閱]** 按鈕。  
  
#### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>若要建立資料驅動訂閱 (SharePoint 模式)  
  
1.  在 SharePoint 文件庫中，將滑鼠停留在報告上方，接著開啟 [選項] 功能表，然後按一下 **[管理訂閱]** 。  
  
2.  按一下 **[加入資料驅動訂閱]** 。  
  
#### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>若要修改現有的資料驅動訂閱 (原生模式)  
  
1.  在 [報表管理員流覽至包含報表的資料夾，將滑鼠停留在報表上，開啟 [選項] 功能表，然後按一下 [**管理**]。  
  
2.  按一下 [**訂閱**] 索引標籤。或者，在報表管理員的頂端上按一下 [**我的訂閱**] 連結  
  
3.  選取您要修改的訂閱。 下列圖示表示資料驅動訂閱：![資料驅動訂閱圖示](../media/hlp-16subscriptiondd.gif "資料驅動訂閱圖示")  
  
#### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>若要修改現有的資料驅動訂閱 (SharePoint 模式)  
  
1.  在 SharePoint 文件庫中，將滑鼠停留在報告上方，接著開啟 [選項] 功能表，然後按一下 **[管理訂閱]** 。  
  
2.  選取您要修改的訂閱。  
  
> [!NOTE]  
>  您可以修改任何已經指定的值。 所有值均以第一次建立時的方式呈現，除了用來存取訂閱者資料存放區的密碼。 每次修改值的時候，都必須在第二頁或任何後續頁面重新輸入密碼。  
  
 在可以建立資料驅動訂閱之前，請先確定有滿足以下需求：  
  
-   **報表需求**。 報表必須使用預存認證或不使用認證，才能在執行階段擷取資料。 如果報表是使用模擬或委派的認證來連接外部資料來源，您便無法訂閱此報表；當處理此訂閱時，將無法使用建立或擁有此訂閱之使用者的認證。 預存認證可以是 Windows 帳戶或資料庫使用者帳戶。 如需詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
     如果「報表產生器」報表是使用模型當做資料來源，而該模型包含模型項目安全性設定，您便無法訂閱此報表。 這項限制中只包含使用模型項目安全性的報表。  
  
     您不能在包含 `User!UserID` 運算式的報表上建立資料驅動訂閱。  
  
-   **資料需求**。 您必須有一個包含訂閱者資料的可存取外部資料來源。  
  
-   **使用者需求**。 此訂閱的作者必須具有「管理報表」和「管理所有訂閱」的權限。 如需項目層級工作權限的詳細資訊，請參閱 [工作和權限](../security/tasks-and-permissions.md)。 此作者也必須具有適當的認證，才能存取包含訂閱者資料的外部資料來源。  
  
##  <a name="define-a-query-that-retrieves-subscription-information"></a><a name="bkmk_define_query"></a>定義可抓取訂閱資訊的查詢  
 資料驅動訂閱必須指定查詢或命令來擷取訂閱者資料， 查詢應該針對每一個訂閱者產生一個資料列。 如果您是使用電子郵件傳遞延伸模組，則查詢應傳回每一個訂閱者的有效電子郵件別名。 傳遞的數目會依據查詢所傳回的資料列數目而定。 如果資料列集包括 10,000 個資料列，則訂閱會傳遞 10,000 個報表。  
  
 如果執行查詢很花時間，您可以增加逾時值以容納更多的處理。  
  
 針對此步驟，您必須在繼續之前先驗證查詢。 驗證並不會處理查詢，但會傳回在資料列集內的所有資料行清單，讓您可以在後續選取範圍中參考資料行。 如果查詢未通過驗證，您就無法繼續。 如果查詢語法不正確或資料來源的連接無效，查詢就無法通過驗證。 使用 **[上一步]** 按鈕，以更正資料來源。  
  
##  <a name="run-a-subscription"></a><a name="bkmk_run_subscription"></a>執行訂用帳戶  
 您需要設定訂閱處理的條件。 您可以設定排程或觸發訂閱，讓更新與報表執行快照集一致。  
  
 ![注意](../media/rs-fyinote.png "注意")雖然使用者介面中沒有可用來立即執行訂閱的功能，但您可以使用簡單的 Windows PowerShell 腳本來觸發要執行的訂閱。 如需詳細資訊，請參閱[使用 PowerShell 變更和列出 Reporting Services 訂用帳戶擁有者和執行訂](manage-subscription-owners-and-run-subscription-powershell.md)用帳戶中的「腳本：執行 (引發) 單一訂閱」一節。  
  
 執行資料驅動訂閱的排程和條件，與標準訂閱的處理相同。  
  
##  <a name="manage-and-delete-a-data-driven-subscription"></a><a name="bkmk_manage_and_delete"></a>管理和刪除資料驅動訂閱  
 您無法透過報表管理員的 [管理作業] 頁面，停止或刪除正在進行中的資料驅動訂閱。 因此，建議您使用共用排程來觸發資料驅動訂閱。 這樣一來，如果您想要暫時防止訂閱處理，就可以暫停觸發訂閱的排程。 如需詳細資訊，請參閱 [建立和管理原生模式報表伺服器的訂閱](../create-manage-subscriptions-native-mode-report-servers.md)。  
  
 若要刪除資料驅動訂閱，請從報表的 [我的訂閱] 頁面或 [訂閱] 頁面選取該訂閱，然後按一下 **[刪除]**。  
  
 如需如何取消資料驅動訂閱的指示，請參閱 [管理執行中的處理序](manage-a-running-process.md)。  
  
## <a name="see-also"></a>另請參閱  
 [以原生模式 &#40;Reporting Services 建立、修改和刪除標準訂閱&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [建立及管理原生模式報表伺服器的訂閱](../create-manage-subscriptions-native-mode-report-servers.md)   
 [訂閱頁面 &#40;報表管理員&#41;](../subscriptions-page-report-manager.md)   
 [我的訂閱頁面 &#40;報表管理員&#41;](../my-subscriptions-page-report-manager.md)  
  
  
