---
title: 其他檔案 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio], miscellaneous
- projects [SQL Server Management Studio], files
- solutions [SQL Server Management Studio], files
- miscellaneous files folder [SQL Server]
ms.assetid: 3c952b0b-8f5f-4d86-9e5d-616c10b9df0d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1f65c04326e791fa3684a06213c3042a42f2f2ab
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702246"
---
# <a name="miscellaneous-files"></a>其他檔案
  任何專案的外部檔案稱為「其他檔案」  (Miscellaneous file)。 您開啟了某個方案之後，便可以開啟和修改關聯於這個專案的其他檔案。 如果副檔名沒有相關的專案程式碼編輯器，這個檔案便會分類為其他檔案。 例如，在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼專案中，會將副檔名為 .txt 或 .mdx 的檔案當作其他檔案來處理。 在 MDX 專案中，副檔名為 .txt 或 .sql 的檔案會當作其他檔案來處理。 若要使副檔名與程式碼編輯器相關聯，請參閱使副檔名與程式[代碼編輯器產生關聯](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)。  
  
 基於許多原因，能夠將其他檔案加入專案中非常有用。 您可能會有某個檔案不一定是已獲辨識的指令碼，但對於方案的開發而言，卻不可或缺。 常見的範例包括開發附註或指示、資料檔，以及程式碼片段。  
  
 其他檔案的運用非常靈活。 例如，假設您有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼專案，其中有許多在資料庫中建立資料表和預存程序的指令碼。 另外，您也有許多資料表的資料檔，副檔名為 .BCP，還有在 README.TXT 檔內的執行指示。 您可以將資料和 README 檔當作其他檔案附加至專案，以便利用專案系統的原始檔控制和其他功能。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 功能表和工具列會隨著所開啟之檔案的格式而不同。 例如，當您開啟文字檔時，會出現 [文字編輯器] 工具列。 如果您開啟 XML 結構描述檔，便會開啟 [XML 結構描述] 工具列。 當您編輯 XML 結構描述時，無法使用 [文字編輯器] 工具列。 當您在專案檔和其他檔案之間切換時，其他檔案的相關命令和工具列會取代所有專案相關命令和工具列。  
  
## <a name="see-also"></a>另請參閱  
 [管理方案和專案的檔案](files-that-manage-solutions-and-projects.md)   
 [解決方案 &#40;SQL Server Management Studio&#41;](solutions-sql-server-management-studio.md)   
 [專案 &#40;SQL Server Management Studio&#41;](projects-sql-server-management-studio.md)  
  
  
