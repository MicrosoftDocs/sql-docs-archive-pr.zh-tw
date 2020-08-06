---
title: 在 SQL Server Data Tools 中建立封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 330e0271421dc620f7c4fad9c6944331ebe94881
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594608"
---
# <a name="create-packages-in-sql-server-data-tools"></a>在 SQL Server 資料工具中建立封裝
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 設計師在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 中建立的封裝將儲存到檔案系統。 若要將封裝儲存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或封裝存放區，您必須儲存該封裝的複本。 如需詳細資訊，請參閱 [儲存封裝的複本](../../2014/integration-services/save-a-copy-of-a-package.md)。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，您可以使用下列其中一個方法來建立新的封裝：  
  
-   使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所包含的封裝範本。  
  
-   使用自訂範本  
  
     若要使用自訂封裝做為建立新封裝的範本，您只需將自訂封裝複製到 DataTransformationItems 資料夾即可。 依預設，這個資料夾位於 C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject。  
  
-   複製現有的封裝。  
  
     如果現有的封裝包含您想重複使用的功能，您可以從其他封裝複製及貼上物件，以加快建立控制流程和新封裝內之資料流程的速度。 如需在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中使用複製及貼上功能的詳細資訊，請參閱 [重複使用封裝物件](reuse-of-package-objects.md)。  
  
     如果您透過複製現有封裝或使用自訂封裝做為範本的方式來建立新封裝，將一併複製現有封裝的名稱和 GUID。 您應該更新這個新封裝的名稱和 GUID，以協助區分新封裝與其複製來源封裝。 例如，如果封裝具有相同的 GUID，在識別記錄資料所屬的封裝時就會發生困難。 您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [屬性] 視窗，重新產生 `ID` 屬性中的 GUID 並且更新 `Name` 屬性的值。 如需詳細資訊，請參閱 [設定封裝屬性](set-package-properties.md) 和 [dtutil 公用程式](dtutil-utility.md)。  
  
-   使用您指定為範本的自訂封裝。  
  
-   執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈  
  
     [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會建立一個完整封裝來進行簡單的匯入或匯出。 此精靈會設定連接、來源和目的地，並加入所需的任何資料轉換，好讓您立即執行匯入或匯出。 您可以選擇儲存封裝以供日後再次執行，或是在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中精簡及增強封裝。 但是，如果您儲存封裝，您必須將封裝加入現有的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，然後才可以在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中變更封裝或執行封裝。  
  
 下列程序將描述如何在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中建立或刪除封裝。  
  
 如需示範如何使用預設封裝範本建立基本封裝的影片，請參閱 [建立基本封裝 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=131023)。  
  
### <a name="to-create-a-package-in-sql-server-data-tools-using-the-package-template"></a>若要在 SQL Server Data Tools 中使用封裝範本來建立封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟您要在其中建立封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝]**** 資料夾，然後按一下 [新增 SSIS 封裝]****。  
  
3.  (選擇性) 將控制流程、資料流程工作和事件處理常式加入封裝。 如需詳細資訊，請參閱[控制流程](control-flow/control-flow.md)、[資料流程](data-flow/data-flow.md)和 [Integration Services &#40;SSIS&#41; 事件處理常式](integration-services-ssis-event-handlers.md)。  
  
4.  在 **[檔案]** 功能表上按一下 **[儲存選取項目]** 以儲存新封裝。  
  
    > [!NOTE]  
    >  您可以儲存空白封裝。  
  
  
