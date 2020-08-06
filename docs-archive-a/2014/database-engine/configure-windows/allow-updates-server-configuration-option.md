---
title: allow updates 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d7e3ede317509a2044be90635db46e30a932af66
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597348"
---
# <a name="allow-updates-server-configuration-option"></a><span data-ttu-id="de2c2-102">允許更新伺服器組態選項</span><span class="sxs-lookup"><span data-stu-id="de2c2-102">allow updates Server Configuration Option</span></span>
  <span data-ttu-id="de2c2-103">此選項仍會出現在 **sp_configure** 預存程序中，但其功能已無法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用。</span><span class="sxs-lookup"><span data-stu-id="de2c2-103">This option is still present in the **sp_configure** stored procedure, although its functionality is unavailable in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="de2c2-104">此設定無效。</span><span class="sxs-lookup"><span data-stu-id="de2c2-104">The setting has no effect.</span></span> <span data-ttu-id="de2c2-105">不支援對系統資料表的直接更新。</span><span class="sxs-lookup"><span data-stu-id="de2c2-105">Direct updates to the system tables are not supported.</span></span>  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 <span data-ttu-id="de2c2-106">變更 **allow updates** 選項將會導致 RECONFIGURE 陳述式失敗。</span><span class="sxs-lookup"><span data-stu-id="de2c2-106">Changing the **allow updates** option will cause the RECONFIGURE statement to fail.</span></span> <span data-ttu-id="de2c2-107">應該從所有指令碼移除對於 **allow updates** 選項的變更。</span><span class="sxs-lookup"><span data-stu-id="de2c2-107">Changes to the **allow updates** option should be removed from all scripts.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="de2c2-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="de2c2-108">See Also</span></span>  
 [<span data-ttu-id="de2c2-109">伺服器組態選項 &#40;SQL Server&#41;</span><span class="sxs-lookup"><span data-stu-id="de2c2-109">Server Configuration Options &#40;SQL Server&#41;</span></span>](server-configuration-options-sql-server.md)  
  
  
