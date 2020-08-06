---
title: 處理選項屬性頁面 (報表管理員) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 28f07c70-7132-4d15-9505-4fdf31dc9cc0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ab43474869eb0b06eba33b4bd597907b7371ce09
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585115"
---
# <a name="processing-options-properties-page-report-manager"></a>處理選項屬性頁面 (報表管理員)
  使用 [處理選項] 屬性頁面可以設定目前選取之報表的報表執行屬性。 這些選項會決定何時進行報表的資料處理。 您可以設定這些選項，以便在離峰時段擷取報表資料。 如果您的報表經常被存取，當多位使用者彼此會在短時間內存取相同的報表時，您就可以暫時快取副本，以避免等待時間。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供報表記錄、執行快照集和快取功能。 如需版本支援的功能清單 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，請參閱[SQL Server 2014 版本支援的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-processing-options-properties-page"></a>若要開啟處理選項屬性頁面  
  
1.  開啟報表管理員，然後找出您想要設定處理屬性的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。 這樣就會開啟該報表的 [一般] 屬性頁面。  
  
4.  選取 **[處理選項]** 索引標籤。  
  
## <a name="options"></a>選項  
 **永遠以最新的資料執行此報表**  
 如果您要在使用者選取報表時擷取報表資料，請使用此選項。 當使用者選取報表時，如果報表有快取副本，則傳回給使用者，否則會執行資料擷取和轉譯。  
  
 選取 **[不要快取此報表的暫存副本]** 就會永遠以最新的資料來執行報表。 開啟報表的每一位使用者都會觸發對資料來源的查詢，這些資料來源包含報表中使用的資料。  
  
 選取 ****，即可在使用者首先開啟報表時，將報表的暫存副本放入快取中。 在快取期間內執行此報表的後續使用者都會收到快取的報表副本。 快取通常會改善效能，因為報表是從快取傳回，而非再次處理。  
  
 快取的報表最後一定會過期。 請指定要儲存快取之報表副本的分鐘數。 一旦暫存副本過期，系統就不會再從快取中傳回報表。 使用者下次開啟報表時，報表伺服器會重新處理報表，並將重新整理過的報表副本存到快取中。  
  
 您也可以使用排程使快取報表過期，以頻率來取代分鐘數。 例如，若要使快取報表在某日結束時過期，可以選取晚上某個特定時間，使副本在超過該時間之後過期。  
  
 **從執行快照集轉譯此報表**  
 使用此選項即可在排程的時間內將已經儲存的報表當做快照集擷取。 當您選擇此選項時，可以將資料處理排程為於離峰時段進行。 不同於使用者開啟報表時才會建立的快取副本，快照集會定期建立而且後續會按照排程重新整理。 快照集不會過期；它們可一直執行服務，直到被較新的版本取代為止。  
  
 由報表執行設定的結果所產生的快照集，與報表記錄快照集具有相同特性。 其差異在於只能有一個報表執行快照集，但潛在地具有許多報表記錄快照集。 報表記錄快照集可從報表的 [記錄] 頁面存取，其中儲存不同的時間點存在之報表的許多執行個體。 相對地，使用者從資料夾存取報表執行快照集的方法，與存取使用中報表的方法相同。 對於報表執行快照集，沒有視覺提示可對使用者指出此報表是快照集。  
  
 若要在您按一下 [套用] 時建立報表快照集，請選取 **[當您在此頁面上按一下 [套用] 按鈕時，會建立報表快照集]** 的相關選項。 這樣就會立即產生報表快照集，使其在排程的起始時間之前就可供使用。  
  
 **報表執行逾時**  
 指定在特定秒數之後報表處理是否逾時。 如果選擇預設值，此報表會使用 [站台設定] 頁面中指定的逾時設定。  
  
 此值會套用至報表伺服器上的報表處理。 它不會針對提供報表資料之資料庫伺服器上的資料處理設定逾時。 不過，您所指定的值必須足以完成資料處理和報表處理。 報表處理的計數在選取報表時會開始，並在開啟報表時結束。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表處理屬性](report-server/set-report-processing-properties.md)   
 [快取多個報表 &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [建立、修改和刪除共用排程](subscriptions/create-modify-and-delete-schedules.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
