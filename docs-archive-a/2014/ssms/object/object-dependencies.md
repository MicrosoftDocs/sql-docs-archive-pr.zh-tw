---
title: 物件相依性 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.common.objectdependencies.f1
ms.assetid: c63d1160-3f3d-45df-99be-6fe081125fb5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 13d1775f1e4e6885fe56a43ce40c4ac155c5b361
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708898"
---
# <a name="object-dependencies"></a>物件相依性
  某些資料庫物件與其他資料庫物件具有相依性。 例如，檢視和預存程序必須相依於特定資料表，這些資料表中包含檢視或程序所傳回的資料。 目前物件的 **物件相依性 (一般頁面)** 列出必須存在，物件才能正常運作的資料庫物件，以及相依於所選物件的物件。 參考自身定義中之其他物件，並將定義儲存在系統目錄中的物件稱為 *參考實體*。 受其他物件參考的物件稱為 *被參考的實體*。  
  
 目前物件的 **物件相依性 (進階頁面)** 列出相依於此物件的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件及 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件。 這些物件可能會儲存在不同的伺服器上。  
  
 在變更或刪除選取的物件之前，請使用此對話方塊來了解相依性。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **相依于的物件**  _\<selected object>_  
 按一下此按鈕會顯示已進行相依性追蹤，並相依於所選取物件的物件清單。  
  
 **物件** _\<selected object>_**相依于**      
 按一下此按鈕會顯示已進行相依性追蹤，所選取物件相依的物件清單。  
  
 **Dependencies** (相依性)  
 按一下**相依於** _\<selected object> 的物件_時，系統會以階層檢視顯示相依於所選物件的物件。 按一下  _\<selected object>_ **所相依的物件**時，系統會以階層檢視顯示所選物件相依的物件。  
  
 **名稱**  
 顯示在上述 [相依性]  樹狀檢視中選取之物件的名稱。  
  
 **型別**  
 顯示在上述 [相依性]  樹狀檢視中選取之物件的類型。  
  
 **上次同步處理時間**  
 > [!NOTE]  
>  只有 [進階]  頁面會提供此選項。  
  
 指定上次更新相依性資訊的時間和日期。  
  
 **相依性類型**  
 > [!NOTE]  
>  只有 [一般]  頁面會提供此選項。  
  
 顯示兩個物件之間的相依性類型。 可以是下列其中一項：  
  
-   結構描述繫結的相依性  
  
     是兩個物件間的關聯性，只要參考物件存在，就可以防止受參考的物件遭到卸除或修改。 使用 WITH SCHEMABINDING 子句建立檢視或使用者自訂函數時，或資料表透過 CHECK 或 DEFAULT 條件約束，或在計算資料行的定義中參考其他物件時，就會建立結構描述繫結的相依性。  
  
-   非結構描述繫結的相依性  
  
     是兩個物件間的關聯性，無法防止受參考的物件遭到卸除或修改。  
  
-   無法使用或未解析的實體  
  
     表示無法判定相依性類型。 只有在選取的物件位於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 前之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的執行個體上時，才會發生這個狀況。  
  
  
