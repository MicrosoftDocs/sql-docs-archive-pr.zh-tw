---
title: 自訂報表項目 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- extending Reporting Services
- Reporting Services, extending
- custom report items
ms.assetid: 64dcaf2c-1af5-4937-8ff7-98f1ec3b367e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86b819cb4d305e537a52a2e7f25cdfa3aefa5f9e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708994"
---
# <a name="custom-report-items"></a>自訂報表項目
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供一組豐富的工具，以建立和發行企業報表、管理安全性與訂閱以及透過完整的 API 來擴充和報告功能。 報表是利用稱為「報表定義語言」(RDL) 的以 XML 為基礎之語言來定義。 RDL 提供描述報表之配置、查詢資訊以及項目類型的指示。 您可以撰寫自訂報表項目來擴充 RDL。 自訂報表項目是由執行階段元件 (由報表處理器在執行階段所呼叫) 以及設計階段元件 (允許在報表設計師中使用自訂報表項目) 所組成。  
  
 如需完全實作的自訂報表項目的範例，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="custom-report-item-scenarios"></a>自訂報表項目案例  
 需要將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到其應用程式的開發人員，可能需要在 RDL 中原本不支援的功能。 這可能包括的項目如：對應控制項、水平清單、單欄式清單以及可再旋轉的矩陣。 執行階段自訂報表項目元件可以使用應用程式來開發和散發以滿足此需求。  
  
 除了提供本來不支援的功能之外，有些開發人員可能會想要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 已隨附的控制項替代版本來擴充現有功能。 在這個案例中，開發人員可以提供三個元件：執行階段元件、設計階段元件以及設計階段報表項目轉換元件 (可依需求將現有的報表項目轉換為自訂報表項目)。  
  
## <a name="in-this-section"></a>本節內容  
 [自訂報表項目架構](custom-report-item-architecture.md)  
 描述組成自訂報表項目的元件。  
  
 [自訂報表項目實作需求](custom-report-item-implementation-requirements.md)  
 描述建立自訂報表項目的必要元件。  
  
 [建立自訂報表項目執行階段元件](creating-a-custom-report-item-run-time-component.md)  
 描述如何建立自訂報表項目執行階段元件。  
  
 [建立自訂報表項目設計階段元件](creating-a-custom-report-item-design-time-component.md)  
 描述如何建立自訂報表項目設計階段元件。  
  
 [操作說明：部署自訂報表項目](how-to-deploy-a-custom-report-item.md)  
 描述如何部署自訂報表項目  
  
 [自訂報表項目類別庫](custom-report-item-class-libraries.md)  
 描述在 `Microsoft.ReportDesigner` 命名空間中自訂報表項目基礎結構類別與 Managed 包裝函數類別  
  
## <a name="see-also"></a>另請參閱  
 [技術參考 &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  
