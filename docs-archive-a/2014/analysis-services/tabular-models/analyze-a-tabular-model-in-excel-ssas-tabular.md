---
title: 在 Excel 中分析方格式模型 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.chooseperspect.f1
ms.assetid: 47fa45fc-60ab-41a1-bde3-5781c8462889
author: minewiskan
ms.author: owend
ms.openlocfilehash: fae542ffb5b470d23d9cf27fcc11367f571e7cec
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598529"
---
# <a name="analyze-a-tabular-model-in-excel-ssas-tabular"></a>在 Excel 中分析表格式模型 (SSAS 表格式)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的 [在 Excel 中進行分析] 功能會開啟 Microsoft Excel、建立模型工作空間資料庫的資料來源連接，以及將樞紐分析表加入工作表。 模型物件 (資料表、資料行、量值、階層和 KPI) 會包含在樞紐分析表欄位清單中當做欄位。  
  
> [!NOTE]  
>  為了使用 [在 Excel 中進行分析] 功能，您必須在與 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]相同的電腦上安裝 Microsoft Office 2003 或更高版本。 如果未將 Office 安裝在相同的電腦上，您可以在其他電腦上使用 Excel，然後連接至模型工作空間資料庫當做資料來源。 然後即可手動將樞紐分析表加入工作表。 模型物件 (資料表、資料行、量值及 KPI) 會包含在樞紐分析表欄位清單中當做欄位。  
  
## <a name="tasks"></a>工作  
  
#### <a name="to-analyze-a-tabular-model-project-by-using-the-analyze-in-excel-feature"></a>若要使用在 Excel 中進行分析功能來分析表格式模型專案  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[在 Excel 中進行分析]**。  
  
2.  在 **[選擇認證和檢視方塊]** 對話方塊中，選取下列其中一個認證選項，以連接至模型工作空間資料來源：  
  
    -   若要使用目前的使用者帳戶，請選取 **[目前的 Windows 使用者]**。  
  
    -   若要使用其他使用者帳戶，請選取 **[其他 Windows 使用者]**。  
  
         此使用者帳戶通常是角色的成員。 不需要密碼。 只能在工作空間資料庫的 Excel 連接環境中使用此帳戶。  
  
    -   若要使用安全性角色，請選取 **[角色]**，然後在清單方塊中選取一個或多個角色。  
  
         您必須使用角色管理員定義安全性角色。 如需詳細資訊，請參閱[建立及管理角色 &#40;SSAS 表格式&#41;](roles-ssas-tabular.md)。  
  
3.  若要使用檢視方塊，請在 **[檢視方塊]** 清單方塊中選取檢視方塊。  
  
     您必須使用 [檢視方塊] 對話方塊定義檢視方塊 (非預設值)。 如需詳細資訊，請參閱[建立和管理 &#40;SSAS 表格式&#41;的觀點](perspectives-ssas-tabular.md)。  
  
> [!NOTE]  
>  當您在模型設計師中變更模型專案時，Excel 的樞紐分析表欄位清單不會自動重新整理。 若要重新整理樞紐分析表欄位清單，請在 Excel 的 **[選項]** 功能區上，按一下 **[重新整理]**。  
  
## <a name="see-also"></a>另請參閱  
 [在 Excel 中進行分析 &#40;SSAS 表格式&#41;](analyze-in-excel-ssas-tabular.md)  
  
  
