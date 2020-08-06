---
title: 快取轉換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.cachetrans.f1
helpviewer_keywords:
- Cache transform
ms.assetid: a5683fc8-9c32-4634-819e-e9815627e4f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 34be3252a3caf344c95e13ae45cc485a8c4ffdc7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597248"
---
# <a name="cache-transform"></a>快取轉換
  「快取轉換」轉換會藉由將資料從資料流程中連接的資料來源寫入至快取連接管理員的方式，產生「查閱轉換」的參考資料集。 「查閱轉換」會藉由聯結已連接資料來源輸入資料行中的資料與參考資料庫中的資料行來執行查閱。  
  
 當您想要設定「查閱轉換」以完整快取模式執行時，可以使用快取連接管理員。 在這個模式中，參考資料集會在「查閱轉換」執行之前載入快取中。  
  
 如需如何透過快取連線管理員和「快取轉換」轉換設定完整快取模式中「查閱轉換」的指示，請參閱 [使用快取連線管理員以完整快取模式實作查閱轉換](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)。  
  
 如需快取參考資料集的詳細資訊，請參閱 [查閱轉換](lookup-transformation.md)。  
  
> [!NOTE]  
>  「快取轉換」只會將唯一的資料列寫入快取連接管理員。  
  
 在單一封裝中，只有「快取轉換」可以將資料寫入至相同的快取連接管理員。 如果封裝包含多個「快取轉換」，則在封裝執行時呼叫的第一個「快取轉換」會將資料寫入連接管理員。 後續「快取轉換」的寫入作業會失敗。  
  
 如需詳細資訊，請參閱 [快取連線管理員](../../connection-manager/cache-connection-manager.md) 和 [快取連線管理員編輯器](../../cache-connection-manager-editor.md)。  
  
## <a name="configuration-of-the-cache-transform"></a>快取轉換的組態  
 您可以將快取連接管理員設定為將資料儲存至快取檔案 (.caw)。  
  
 您可以利用下列方式設定「快取轉換」：  
  
-   指定快取連接管理員。  
  
-   將「快取轉換」中的輸入資料行對應至快取連接管理員中的目的地資料行。  
  
    > [!NOTE]  
    >  每個輸入資料行都必須對應至目的地資料行，而資料行資料類型也必須相符； 否則，「 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 設計師」會顯示錯誤訊息。  
  
     您可以使用 [快取連線管理員編輯器]  修改資料行資料類型、名稱和其他資料行屬性。  
  
 您可以透過 [ [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 設計師] 設定屬性。 如需可在 [進階編輯器]  對話方塊中設定之屬性的詳細資訊，請參閱[轉換自訂屬性](transformation-custom-properties.md)。  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 轉換](integration-services-transformations.md)   
 [資料流程](../data-flow.md)  
  
  
