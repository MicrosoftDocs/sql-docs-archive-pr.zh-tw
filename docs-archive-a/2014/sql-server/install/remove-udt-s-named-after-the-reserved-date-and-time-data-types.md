---
title: 移除以保留的日期和時間資料類型命名的 UDT&#39;|Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- time data type [SQL Server], UDTs
- date data type [SQL Server], UDTs
ms.assetid: 48f109af-b1d1-4f03-a7e3-8a0b05ed94e8
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 827f060b309a7a620fd448554b074f45d78d3cb0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598146"
---
# <a name="remove-udt39s-named-after-the-reserved-date-and-time-data-types"></a>移除以保留的日期和時間資料類型命名的 UDT&#39;
  Upgrade Advisor 偵測到依據針對 `date` 或 `time` 資料類型保留之詞彙所命名的使用者定義型別 (UDT)。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 用於資料類型的詞彙不應該當做 Common Language Runtime (CLR) 或別名 UDT 的名稱使用。  
  
## <a name="corrective-action"></a>更正動作  
 請移除依據此資料類型所命名的 UDT，然後使用未保留的名稱重新建立 UDT。  
  
  
