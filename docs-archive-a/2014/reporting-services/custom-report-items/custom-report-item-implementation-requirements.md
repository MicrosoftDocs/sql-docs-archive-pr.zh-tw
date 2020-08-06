---
title: 自訂報表項目實作需求 | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 69fdf58eb385e819b524b9c5b5178997257c797c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709002"
---
# <a name="custom-report-item-implementation-requirements"></a>自訂報表項目實作需求
  本主題將討論開發和部署自訂報表項目的必要條件。  
  
## <a name="development-and-deployment-requirements"></a>開發和部署需求  
 為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 開發自訂報表項目需要下列項目：  
  
-   使用和執行之伺服器的系統管理存取權 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 。  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)]或更新版本，且 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 已安裝軟體發展工具組 (SDK) 。  
  
-   存取 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件集。  
  
-   熟悉 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的元件製做與元件模型命名空間。 如需相關資訊，請參閱 msdn.microsoft.com 上面的＜元件撰寫＞與＜在 Visual Studio 中的元件模型命名空間＞。  
  
## <a name="language-and-namespace-requirements"></a>語言與命名空間需求  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自訂報表項目完全支援 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。 您可以使用所選的 .NET 相容語言來開發自訂報表項目。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 提供開發人員許多工具與功能，以簡化和加速程式碼撰寫、偵錯和測試的反覆循環，並使部署更加容易。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 包括 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 與 C# 編譯器及相關工具。  
  
-   自訂報表項目使用 `Microsoft.ReportDesigner` 與 <xref:Microsoft.ReportingServices.Interfaces> 命名空間。 這些是儲存在 Microsoft.ReportingServices.Designer.DLL 與 Microsoft.ReportingServices.Interfaces.DLL 組件中，是以 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的一部分來安裝。  
  
-   自訂報表項目設計階段元件需要從 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 <xref:System.ComponentModel> 命名空間實作介面。 <xref:System.ComponentModel> 記載於 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件集中。  
  
> [!IMPORTANT]  
>  依預設，[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 會隨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起安裝，但是不會安裝 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。 除非已在電腦上安裝 SDK，而且 SDK 文件集是包含在線上叢書集合中，否則本節中的 SDK 內容連結將不會有任何作用。 在安裝 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 之後，您可以遵循[新增或移除 SQL Server 的產品文件集](../../index.yml)中的指示，將 SDK 文件集新增至線上叢書集合和目錄。  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂報表專案執行時間元件](creating-a-custom-report-item-run-time-component.md)   
 [建立自訂報表專案設計階段元件](creating-a-custom-report-item-design-time-component.md)   
 [如何：部署自訂報表專案](how-to-deploy-a-custom-report-item.md)   
 [自訂報表項目類別庫](custom-report-item-class-libraries.md)  
  
  
