---
title: '[加入 Cube 維度] 對話方塊 (Analysis Services-多維度資料) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.addcubedimensiondialog.f1
helpviewer_keywords:
- Add Cube Dimension dialog box
ms.assetid: 625a3b1f-183b-445f-9bb7-96945c324767
author: minewiskan
ms.author: owend
ms.openlocfilehash: d0de75c02c39b0690184f35f2b0b6a07d7ed9a4f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592345"
---
# <a name="add-cube-dimension-dialog-box-analysis-services---multidimensional-data"></a>加入 Cube 維度對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [加入 Cube 維度]**** 對話方塊，即可將資料庫維度的參考加入 Cube。 您可以執行下列其中一個動作，來顯示 [加入 Cube 維度]**** 對話方塊：  
  
-   在 Cube 設計師之 [Cube 結構]**** 或 [維度使用方式]**** 索引標籤的 [工具列]**** 窗格中，按一下 [加入 Cube 維度]****。  
  
-   在 Cube 設計師的 [Cube 結構]**** 索引標籤上，以滑鼠右鍵按一下 [維度]**** 窗格，然後從操作功能表中選取 [加入 Cube 維度]****。  
  
-   在 Cube 設計師的 [維度使用方式]**** 索引標籤上，以滑鼠右鍵按一下 [方格]**** 窗格，然後從操作功能表中選取 [加入 Cube 維度]****。  
  
> [!NOTE]  
>  每個 Cube 維度對量值群組只能有一個關聯性。 不過，如果 Cube 維度所依據的資料庫維度，在資料來源檢視中透過一個以上的關聯性與量值群組相關，則您可以建立一個以上的 Cube 維度並將其加入至 Cube。 此類維度被稱為角色扮演維度，且一般是和時間維度一起發生。  
  
## <a name="options"></a>選項  
 **選取維度**  
 選取現有的資料庫維度，即可將依據此資料庫維度的 Cube 維度加入至選取的 Cube。 從相同資料庫維度中可以定義多個 Cube 維度。  
  
> [!NOTE]  
>  如果有依據相同資料庫維度之一個以上的 Cube 維度加入至一個 Cube，則其他的 Cube 維度會被稱為角色扮演維度。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
