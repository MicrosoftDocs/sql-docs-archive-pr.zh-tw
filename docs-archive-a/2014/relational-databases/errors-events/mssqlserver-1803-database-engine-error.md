---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 11302f882846c49c6e9998608967e7042ac9860c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597155"
---
# <a name="mssqlserver_1803"></a>MSSQLSERVER_1803
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1803|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NO_SPACE|  
|訊息文字|CREATE DATABASE 失敗。 主要檔案至少要有 %d MB，才能容納模型資料庫的副本。|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立模型資料庫的複本來建立資料庫。 然後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將此複本重新命名，並將新的資料庫放大為所要求的大小。 在此情況下，使用者嘗試建立小於模型資料庫的資料庫。 由於模型資料庫的複本不適合主要資料檔案 (因為檔案小於此模型資料庫)，所以此作業失敗。  
  
## <a name="user-action"></a>使用者動作  
 使用較大的資料庫檔案大小建立資料庫。 然後如果您想要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 DBCC SHRINKDATABASE 陳述式，請縮小資料庫。  
  
  
