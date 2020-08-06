---
title: SQL Server 版本的計算容量限制 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- processors [SQL Server], supported
- number of processors supported
- maximum number of processors supported
ms.assetid: cd308bc9-9468-40cc-ad6e-1a8a69aca6c8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f098b019205417d0339f426832c5683e6b8fa7cc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595608"
---
# <a name="compute-capacity-limits-by-edition-of-sql-server"></a>SQL Server 版本的計算容量限制
  本主題討論不同 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本的計算容量限制以及它們在具有超執行緒處理器的實體和虛擬化環境中有何差異。  
  
 ![對應至計算容量限制](../../2014/getting-started/media/compute-capacity-limits.gif "對應至計算容量限制")  
  
 下表描述上圖所使用的註解：  
  
|值|描述|  
|-----------|-----------------|  
|0..1|零個或一個|  
|1|只有一個|  
|1..*|一個或多個|  
|0..*|零個或多個|  
|1..2|一個或兩個|  
  
> [!IMPORTANT]
>  詳細說明：  
> 
>  1.  一個虛擬機器會被配置一個或多個虛擬處理器。  
> 2.  一個或多個虛擬處理器只會配置給一個虛擬機器。  
> 3.  零個或一個虛擬處理器會對應至零個或多個邏輯處理器。 當虛擬處理器與邏輯處理器的對應為：  
> 
>      -   一對零時，表示客體作業系統並未使用的未繫結邏輯處理器。  
>     -   一對多時，表示過度認可。  
>     -   零對多時，表示虛擬機器不存在主機系統上，因此 VM 並未使用任何邏輯處理器。  
> 4.  一個插槽會對應至零個或多個核心。 當插槽與核心的對應為：  
> 
>      -   一對零時，表示空的插槽 (未安裝晶片)。  
>     -   一對一時，表示安裝至插槽的單核心晶片 (目前非常少見)。  
>     -   一對多時，表示安裝至插槽的多核心晶片 (一般的值為 2、4、8)。  
> 5.  一個核心會對應至一個或兩個邏輯處理器。 當核心與邏輯處理器的對應為：  
> 
>      -   一對一時，表示超執行緒已關閉。  
>     -   一對二時，表示超執行緒已開啟。  
  
 下列定義適用於本主題中使用的詞彙：  
  
-   從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、作業系統、應用程式或驅動程式的觀點而言，執行緒或邏輯處理器都是單一邏輯運算引擎。  
  
-   一個核心是指一個處理處理器單元，可能是由一個或多個邏輯處理器組成。  
  
-   一個實體處理器可能是由一個或多個核心組成。 實體處理器與處理器封裝或插槽相同。  
  
 具有多個實體處理器的系統或是具有多核心及/或超執行緒之實體處理器的系統可讓作業系統同時執行多個工作。 每個執行的執行緒都會顯示成邏輯處理器。 例如，如果您有一部具備兩個啟用超執行緒之四核心處理器的電腦，而且每個核心都有兩個執行緒，則總共有 16 個邏輯處理器：2 個處理器 x 4 個核心 (每個處理器) x 2 個執行緒 (每個核心)。 請注意：  
  
-   來自超執行緒核心之單一執行緒的邏輯處理器計算容量小於來自停用超執行緒之相同核心的邏輯處理器計算容量。  
  
-   但是，超執行緒核心中 2 個邏輯處理器的計算容量大於停用超執行緒之相同核心的計算容量。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的每個版本都有兩個計算容量限制：  
  
1.  插槽的數目上限 (與實體處理器、插槽或處理器封裝相同)。  
  
2.  作業系統所報告的核心數目上限。  
  
 這些限制適用於單一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。 它們代表單一執行個體將會使用的計算容量上限。 但是，它們不會限制可部署執行個體的伺服器。 實際上，在相同的實體伺服器上部署多個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體可以有效地使用插槽及/或核心數目超過下列容量限制之實體伺服器的運算容量。  
  
 下表指定每個 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]版本之單一執行個體的計算容量限制：  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|單一執行個體所使用的計算容量上限 ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)])|單一執行個體所使用的計算容量上限 (AS、RS)|  
|---------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
|Enterprise Edition：以核心為基礎的授權<sup>1</sup>|作業系統最大值|作業系統最大值|  
|開發人員|作業系統最大值|作業系統最大值|  
|評估|作業系統最大值|作業系統最大值|  
|商業智慧|限制為 4 個插槽或 16 個核心的較小者|作業系統最大值|  
|標準|限制為 4 個插槽或 16 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|  
|Web|限制為 4 個插槽或 16 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|  
|Express|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|  
|Express with Tools|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|  
|Express with Advanced Services|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|  
  
 <sup>1</sup> Enterprise Edition （含伺服器 + 用戶端存取許可證） (CAL) 授權 (不適用於新的合約) 限制為每個實例最多20個核心 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 核心伺服器授權模式之下沒有任何限制。  
  
 在虛擬化環境中，計算容量限制是以邏輯處理器 (而非核心) 的數目為基礎，因為客體應用程式看不見處理器架構。  例如，如果一部伺服器的四個插槽都插入四核心處理器，而且能夠針對每個核心啟用兩個超執行緒，則在啟用超執行緒的情況下，總共包含 32 個邏輯處理器，但是在停用超執行緒的情況下，只包含 16 個邏輯處理器。 這些邏輯處理器可對應至伺服器上的虛擬機器，而該邏輯處理器上的虛擬機器計算負載會對應到主機伺服器中實體處理器上的執行執行緒。  
  
 當每個虛擬處理器的效能都很重要時，您可能會想要停用超執行緒。 雖然您可以在 BIOS 設定期間使用處理器的 BIOS 設定來啟用或停用超執行緒，不過這種伺服器範圍的作業通常會影響伺服器上執行的所有工作負載。 因此，建議您分隔在虛擬化環境中執行的工作負載以及實體作業系統環境中可從超執行緒效能提升獲益的工作負載。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 的版本和元件](../sql-server/editions-and-components-of-sql-server-2016.md)   
 [SQL Server 2014 版本所支援的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server 的最大容量規格](../sql-server/maximum-capacity-specifications-for-sql-server.md)   
 [SQL Server 2014 快速入門安裝](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
