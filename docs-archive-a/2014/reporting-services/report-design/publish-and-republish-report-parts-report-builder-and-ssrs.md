---
title: 發行與重新發行報表組件 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 92dce484-f39b-403c-9caf-d8772bc3aca3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 95fd5e3f7519c6a0d4a6f08cb9bcbf2507d32aaa
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594384"
---
# <a name="publish-and-republish-report-parts-report-builder-and-ssrs"></a>發行與重新發行報表組件 (報表產生器及 SSRS)
  您可以使用預設值在預設位置發行報表組件，或者您可以編輯報表組件中繼資料 (例如名稱和描述)，並將其儲存在報表伺服器的其他位置。 如果您有正確的權限，也可以將其儲存到與報表伺服器整合的 SharePoint 網站。  
  
 您可以只發行相依之資料集內嵌在其中的報表組件，或者您可以個別發行資料集。 如果個別發行資料集，它會變成共用資料集，而且報表組件會連結到該資料集。 如需詳細資訊，請參閱 [報表產生器中的報表組件和資料集](../report-data/report-parts-and-datasets-in-report-builder.md)。  
  
 您可以重新發行現有的報表組件。 如果您有權限，即使您沒有建立報表組件，也可以加以儲存以覆寫伺服器上報表組件的原始執行個體。 您也可以將它發行為新的報表組件，並儲存在相同或不同的位置。  
  
### <a name="to-publish-a-report-part"></a>若要發行報表組件  
  
1.  在 [報表產生器] 功能表上，按一下 [發行報表組件]****。  
  
     如果您沒有連接到報表伺服器，系統會提示您連接。 如果您無法連接到報表伺服器，就無法啊型報表組件。  
  
2.  若要使用預設值將報表組件儲存至預設位置，請按一下 [使用預設值發行所有報表組件]****。  
  
     否則，按一下 [發行前檢閱並修改報表組件]****。  
  
3.  編輯報表組件名稱和描述：按兩下名稱可以編輯名稱，而在 [描述]**** 欄位中按一下則可新增描述。  
  
    > [!NOTE]  
    >  最好提供報表組件名稱和描述，以協助使用者在搜尋時識別它。 若是完整路徑，報表組件名稱的最大長度為 260 個字元，包括伺服器上的資料夾名稱，後面接著報表組件的實際名稱。  
  
4.  若要將報表組件儲存至預設值之外的其他資料夾中，請按一下 [瀏覽]**** 按鈕。  
  
5.  完成設定報表中所有報表組件的選項時，請按一下 [發行]****。  
  
     發行報表組件之後，對話方塊會顯示成功發行的報表組件，以及未成功發行的報表組件。 您可以在 [發行報表組件]**** 對話方塊中，檢視無法發行之報表組件的詳細資料。  
  
6.  按一下 **關閉**。  
  
### <a name="to-republish-a-report-part"></a>重新發行報表組件  
  
1.  請遵循先前的程序發行報表組件。  
  
2.  在 [發行報表組件]**** 對話方塊中，如果您按一下 [發行為報表組件的新複本]****，報表產生器就不會覆寫伺服器上現有的報表組件，但是會建立另一個報表組件。  
  
> [!NOTE]  
>  如果您將其發行為新的報表組件，它將會擁有一個新的唯一識別碼。 如果原始報表組件變更，它不會再接收更新。  
  
## <a name="see-also"></a>另請參閱  
 [報表元件 &#40;報表產生器和 SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [報表產生器中的報表元件和資料集](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [&#40;報表產生器和 SSRS&#41;疑難排解報表元件](../troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [檢查是否有更新，或關閉 &#40;報表產生器和 SSRS 的更新&#41;](../check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)   
 [瀏覽報表組件及設定預設資料夾 &#40;報表產生器及 SSRS&#41;](browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
  
