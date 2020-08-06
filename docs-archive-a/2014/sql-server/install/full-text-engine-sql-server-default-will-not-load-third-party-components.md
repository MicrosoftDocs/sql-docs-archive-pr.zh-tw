---
title: 適用于 SQL Server 的 Microsoft 全文檢索引擎不會預設載入未簽署的協力廠商元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Full-Text Engine for SQL service
- MSFTESQL service
ms.assetid: 029f9895-7232-4149-9362-3ab1a4133d21
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 12ff188fb6aa6ac286817a7cc1c3ad726483c886
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607248"
---
# <a name="the-microsoft-full-text-engine-for-sql-server-will-not-load-unsigned-third-party-components-by-default"></a><span data-ttu-id="f50ab-102">Microsoft Full-Text Engine for SQL Server 預設不會載入未簽署的協力廠商元件</span><span class="sxs-lookup"><span data-stu-id="f50ab-102">The Microsoft Full-Text Engine for SQL Server will not load unsigned third-party components by default</span></span>
  <span data-ttu-id="f50ab-103">根據預設，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會載入未經 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 簽署的元件。</span><span class="sxs-lookup"><span data-stu-id="f50ab-103">By default, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] will not load components that are not signed by [!INCLUDE[msCoName](../../includes/msconame-md.md)].</span></span>  
  
## <a name="component"></a><span data-ttu-id="f50ab-104">元件</span><span class="sxs-lookup"><span data-stu-id="f50ab-104">Component</span></span>  
 <span data-ttu-id="f50ab-105">全文檢索搜尋</span><span class="sxs-lookup"><span data-stu-id="f50ab-105">Full-Text Search</span></span>  
  
## <a name="description"></a><span data-ttu-id="f50ab-106">描述</span><span class="sxs-lookup"><span data-stu-id="f50ab-106">Description</span></span>  
 <span data-ttu-id="f50ab-107">升級之後，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設不會載入目前安裝在伺服器上的協力廠商篩選，例如 PDF 篩選。</span><span class="sxs-lookup"><span data-stu-id="f50ab-107">A third-party filter, such as a PDF filter, that is currently installed on the server will not be loaded by the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] by default after upgrade.</span></span>  
  
## <a name="corrective-action"></a><span data-ttu-id="f50ab-108">更正動作</span><span class="sxs-lookup"><span data-stu-id="f50ab-108">Corrective Action</span></span>  
 <span data-ttu-id="f50ab-109">若要載入協力廠商篩選，您必須設定*load_os_resource* ，並關閉該實例上的*verify_signature* 。</span><span class="sxs-lookup"><span data-stu-id="f50ab-109">To load a third party filter, you must set *load_os_resource* and turn off *verify_signature* on that instance.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f50ab-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f50ab-110">See Also</span></span>  
 [<span data-ttu-id="f50ab-111">使用升級建議程式</span><span class="sxs-lookup"><span data-stu-id="f50ab-111">Working with Upgrade Advisor</span></span>](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
