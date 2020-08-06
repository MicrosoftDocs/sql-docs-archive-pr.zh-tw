---
title: 在90或更新版本的相容性模式中，CREATE STATISTICS 語句中不支援 WITH ROWS |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d28a05e7cd025e213e2cebdce9d582a9df446fea
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595385"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>在 90 或之後的相容性模式中，CREATE STATISTICS 陳述式中不支援 WITH ROWS
  當您執行相容性模式設定為 90 或之後的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，系統不支援在 CREATE STATISTICS 陳述式中指定 WITH ROWS。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 藉由使用範例*數目*資料列來指定，或指定符合記載語法的其他選項，以修改包含資料列的 CREATE STATISTICS 語句。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜CREATE STATISTICS (Transact-SQL)＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
