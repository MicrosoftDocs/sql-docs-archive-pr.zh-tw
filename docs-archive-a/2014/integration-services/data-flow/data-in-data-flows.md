---
title: 資料流程中的資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- comparing data
- data types [Integration Services], data flow
- parsing [Integration Services]
- string comparisons
- data flow [Integration Services], data options
ms.assetid: 8a9d6186-eb52-48e3-997e-021f24d458a3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a073db65768c413b6cbe648c757ad75d80bd318e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708513"
---
# <a name="data-in-data-flows"></a>資料流程中的資料
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供一組資料流程中使用的資料類型。  
  
## <a name="data-type-conversion"></a>資料類型轉換  
 加入資料流程中的來源可以將來源資料轉換為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。 後續轉換可以將資料轉換為不同的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型，而根據載入資料之資料存放區的類型，目的地可以將最終 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型轉換為目的地資料存放區所要求的資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](integration-services-data-types.md)。  
  
 如果要將資料轉換為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型，資料流程元件會剖析資料。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供快速剖析與標準剖析兩種資料剖析類型。 大部分的資料流程元件僅可以使用標準剖析；但是，「一般檔案」來源和「資料轉換」既可以使用快速剖析，也可以使用標準剖析。 如需詳細資訊，請參閱 [剖析資料](parsing-data.md)。  
  
## <a name="data-type-comparison"></a>資料類型比較  
 許多轉換會比較資料值。 例如，「彙總」轉換對值進行比較是為了彙總一組資料列的值，「排序」轉換對值進行比較是為了將其排序，而「查閱」轉換則是在個別參考資料表中將值互相進行比較。 為了指定應如何比較字串，轉換會包含一組比較選項，例如是否忽略區分大小寫、如何處理日語文字中的假名類型，以及是否忽略字串中的空白字元。 如需詳細資訊，請參閱 [Comparing String Data](comparing-string-data.md)。  
  
 運算式評估工具還會在評估變數、優先順序條件約束及轉換所使用的運算式時，對資料值進行比較。  
  
## <a name="data-flow-troubleshooting"></a>資料流程疑難排解  
 將封裝部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄之後，您可以在執行期間分析封裝中的資料流程，以檢查效能或尋找其他問題。 可使用標準報表查看封裝狀態及記錄，並可以查詢資料庫檢視以取得執行封裝的詳細資訊。 您還可以在執行期間動態地加入及刪除資料點選，以鎖定您封裝的某個特定元件。 如需詳細資訊，請參閱 [資料流程分析](data-flow.md)。  
  
  
