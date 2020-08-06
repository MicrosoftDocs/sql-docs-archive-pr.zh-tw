---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 32ae8ebe102008d08a6059328ed57cd118ece019
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606333"
---
# <a name="localdb_error_instance_folder_path_too_long"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|260|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|本機資料庫執行個體資料夾的完整路徑長度比 MAX_PATH 還長。 實例必須儲存在資料夾：%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server 本機 DB\Instances \\<實例名稱 \> 。|  
  
## <a name="explanation"></a>說明  
 應儲存執行個體的路徑長度超過 MAX_PATH。  
  
## <a name="user-action"></a>使用者動作  
 請建立長度短於 MAX_PATH 的新路徑。  
  
  
