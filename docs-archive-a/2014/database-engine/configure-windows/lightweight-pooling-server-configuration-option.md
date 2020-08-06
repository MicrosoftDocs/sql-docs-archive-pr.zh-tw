---
title: 輕量型共用伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default lightweight pooling
- decreasing overhead
- lightweight pooling option
- system overhead [SQL Server]
- performance [SQL Server], lightweight pooling
- context switching [SQL Server], lightweight pooling option
- excessive context switching [SQL Server]
- reducing overhead
- overhead [SQL Server]
ms.assetid: 2dc11b61-d065-4126-8e00-acf40390f9fb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 549ff7451a31b48459b5a290b94ad406c3768a91
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596902"
---
# <a name="lightweight-pooling-server-configuration-option"></a>輕量型共用伺服器組態選項
  在對稱式多處理 (SMP) 環境中，有時候會出現內容切換過多的現象，[輕量型共用] 選項可用來減少這種現象對系統所造成的額外負擔。 發生內容切換過多的現象時，輕量型共用可以執行內容切換內嵌，藉此幫助減少使用者/核心的環狀轉換，而提供較佳的效能。  
  
 Fiber 模式適用於 UMS 工作者的環境切換是重大效能瓶頸的某些狀況。 因為這個狀況非常罕見，所以 Fiber 模式幾乎不太會提高一般系統上的效能或延展性。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 中改善的環境切換也減少了 Fiber 模式需求。 我們不建議您針對例行作業使用 Fiber 模式排程。 這是因為 Fiber 模式可能會抑制內容切換通常會有的好處而降低效能，而且使用執行緒本機存放裝置 (TLS) 或執行緒擁有之物件 (例如 Win32 核心物件) 的某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件無法在 Fiber 模式下正確運作。  
  
 將 **lightweight pooling** 設成 1 會使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 切換成 Fiber 模式排程。 這個選項的預設值是 0。  
  
 **lightweight pooling** 屬於進階選項。 如果您要使用 **sp_configure** 系統預存程序來變更此設定，只有當 **show advanced options** 設為 1 時，才能變更 **lightweight pooling** 。 伺服器重新啟動之後，設定才會生效。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows XP 不支援輕量型共用。 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 提供了輕量型共用的完整支援。  
  
> [!NOTE]  
>  輕量型共用不支援 Common Language Runtime (CLR) 的執行。 停用下列兩個選項的其中一個："clr enabled" 或 "lightweight pooling"。 依賴 CLR 而且在 Fiber 模式下無法正常運作的功能包括了階層資料類型、複寫和以原則為基礎的管理。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 已啟用伺服器組態選項](clr-enabled-server-configuration-option.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CLR 已啟用伺服器組態選項](clr-enabled-server-configuration-option.md)  
  
  
