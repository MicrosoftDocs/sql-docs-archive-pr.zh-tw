---
title: 附加和卸離 Analysis Services 資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssms.detachdatabase.f1
- sql12.asvs.ssms.attachdatabase.f1
- sql12.asvs.ssmsimbi.AttachDatabase.f1
- sql12.asvs.ssmsimbi.DetachDatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
author: minewiskan
ms.author: owend
ms.openlocfilehash: cd72277970605691e06f3baacf167ea135343b3f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606457"
---
# <a name="attach-and-detach-analysis-services-databases"></a>附加和卸離 Analysis Services 資料庫
  通常在很多情況下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫管理員 (dba) 會想要讓資料庫保持離線一段時間，然後在相同或不同的伺服器執行個體上，讓該資料庫恢復連線狀態。 這些情況通常是由商務需求所驅使，例如將資料庫移至不同的磁碟以提升效能、取得讓資料庫成長的空間，或升級產品。 對於所有這些案例和其他情況， `Attach` 和 `Detach` 命令可讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba 讓資料庫離線，並輕鬆地使其恢復上線。  
  
## <a name="attach-and-detach-commands"></a>Attach 和 Detach 命令  
  命令可讓您將離線的資料庫恢復連線狀態。 您可以將資料庫附加至原始伺服器執行個體或其他執行個體。 當您附加資料庫時，使用者可以指定資料庫的 **[ReadWriteMode]** 設定。  命令可讓您中斷資料庫與伺服器的連線。  
  
## <a name="attach-and-detach-usage"></a>Attach 和 Detach 使用方式  
  命令是用來讓現有的資料庫結構恢復連線狀態。 如果資料庫是以 `ReadWrite` 模式附加，它就只能附加至伺服器執行個體一次。 不過，如果資料庫是以 `ReadOnly` 模式附加，它就可以附加至不同的伺服器執行個體許多次。 不過，相同的資料庫無法附加至相同的伺服器執行個體超過一次。 當您嘗試附加相同的資料庫超過一次時，即使資料已經複製到個別的資料夾，還是會引發錯誤。  
  
> [!IMPORTANT]  
>  如果需要使用密碼才能卸離資料庫，則附加資料庫時也會需要使用相同的密碼。  
  
  命令是用來讓現有的資料庫結構保持離線。 卸離資料庫時，您應該提供密碼來保護機密中繼資料。  
  
> [!IMPORTANT]  
>  為了保護資料檔案的內容，您應該針對資料夾、子資料夾和資料檔案使用存取控制清單。  
  
 當您卸離資料庫時，伺服器會遵循下列步驟進行。  
  
|卸離讀取/寫入資料庫|卸離唯讀資料庫|  
|--------------------------------------|-------------------------------------|  
|1) 伺服器發出在資料庫上執行 CommitExclusive 鎖定的要求<br />2) 伺服器等候直到所有進行中的交易都已認可或回復為止<br />3) 伺服器建立卸離資料庫所需的所有中繼資料<br />4) 資料庫標示為已刪除<br />5) 伺服器認可交易|1) 資料庫標示為已刪除<br />2) 伺服器認可交易<br /><br /> <br /><br /> 注意：您無法針對唯讀資料庫變更卸離密碼。 如果您針對已經包含密碼的卸離資料庫提供密碼參數，就會引發錯誤。|  
  
  和  命令必須當做單一作業執行。 它們無法在同一個交易中與其他作業結合。 此外， `Attach` 和 `Detach` 命令是不可部分完成的交易式命令。 這表示此作業不是成功，就是失敗。 沒有任何資料庫會處於未完成的狀態。  
  
> [!IMPORTANT]  
>  您必須擁有伺服器或資料庫管理員權限才能執行 `Detach` 命令。  
  
> [!IMPORTANT]  
>  您必須擁有伺服器管理員權限才能執行 `Attach` 命令。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 [Microsoft.analysisservices。卸離 *](/dotnet/api/microsoft.analysisservices.core.database.detach)   
 [移動 Analysis Services 資料庫](move-an-analysis-services-database.md)   
 [資料庫 Readwritemode](database-readwritemodes.md)   
 [在 ReadOnly 和 ReadWrite 模式之間切換 Analysis Services 資料庫](switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Detach 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Attach 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  
