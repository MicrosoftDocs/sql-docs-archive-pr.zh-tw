---
title: 儲存套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 102e2c3eab001c230722bf3485d6ea9731aa99a5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706585"
---
# <a name="save-packages"></a>儲存封裝
  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，您可以使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師來建立封裝，並將封裝儲存為檔案系統中的 XML 檔案 (.dtsx 檔案)。 您也可以將封裝 XML 檔案的複本儲存至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 msdb 資料庫，或儲存至封裝存放區。 封裝存放區代表 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務所管理之檔案系統位置中的資料夾。  
  
 如果您將封裝儲存至檔案系統，可以在稍後使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務將封裝匯入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或匯入封裝存放區。 如需詳細資訊，請參閱[匯入和匯出封裝 &#40;SSIS 服務&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)。  
  
 您也可以使用命令提示字元公用程式 **dtutil**，在檔案系統與 msdb 之間複製封裝。 如需詳細資訊，請參閱 [dtutil Utility](dtutil-utility.md)。  
  
### <a name="to-save-a-package"></a>若要儲存封裝  
  
-   [將封裝儲存至檔案系統](../../2014/integration-services/save-a-package-to-the-file-system.md)  
  
-   [儲存封裝的複本](../../2014/integration-services/save-a-copy-of-a-package.md)  
  
  
