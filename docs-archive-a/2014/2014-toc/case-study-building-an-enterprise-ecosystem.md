---
title: 案例研究：使用 Microsoft Dynamics ERP 和 SQL Server 2014 複寫來建立企業生態系統，以提供擴充性和效能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 2b0b5ab7-4e08-431a-bd59-360177c4565c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: dfde59b5e3e12746aa6dbaf975b079cfe32a3718
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584861"
---
# <a name="case-study-building-an-enterprise-ecosystem-with-microsoft-dynamics-erp-and-sql-server-2014-replication-for-scalability-and-performance"></a>案例研究：使用 Microsoft Dynamics ERP 和 SQL Server 2014 複寫建置具有延展性和效能的企業生態系統。

  **摘要：** 本白皮書涵蓋下列案例：  
如何使用 SQL Server 2014 中的異動複寫，將 Dynamics AX 用戶端之間的交易散發到多個節點。 因為資料為跨節點進行即時維護，所以異動複寫提供資料備援來增加資料的可用性，包含可用來讓效能分析更有效率的資料。  
如何在運用異動複寫來建置 Microsoft Dynamics ERP 中高擴充性的企業生態系統時，了解所涉及的詳細規格。 提供高效能和延展性，且不需自訂 AX 的立即可用功能。  
  
 異動複寫一般用於需要高輸送量的伺服器對伺服器工作流程中。 這些包含案例，例如提升延展性和可用性、資料倉儲和報表、整合多個站台的資料、整合異質資料，以及卸載批次處理。 這份技術白皮書描述一個相異案例及相關聯的模式，內容為在 Microsoft Dynamics ERP 中運用異動複寫。 其還包含在考慮以異動複寫建置企業資源規劃 (ERP) 特定的企業解決方案時，所會遇到的挑戰和最佳作法，以及不同階段的效能分析。  
  
 此內容適用於開發人員、架構設計人員和資料庫管理員。 這是假設這份技術白皮書的讀者具備 SQL Server 2008、2012 或 2014 以及 SQL Server 管理經驗的基本知識。  
  
 **寫入器：** Prabhakaran Sethuraman (PRAB) ，Microsoft  
  
 **技術審核者：** Prabhakaran Sethuraman (PRAB) ，Microsoft;Santosh Padhy，Microsoft;Pavel Majstrov，Microsoft;Karthik Sankaranarayanan，Microsoft;Jon Acone，Microsoft;David Stahlkopf，Microsoft;Kent Oldenburger，Microsoft;Mandi Ohlinger，Microsoft;Jason Roth，Microsoft  
  
 **已發行：** 2015年10月  
  
 **適用物件：** SQL Server 2008、SQL Server 2012 及 SQL Server 2014  
  
 若要查看檔，請下載  
        [案例研究：使用 Microsoft DYNAMICS ERP 和 SQL Server 2014 複寫來建立企業生態系統，以提供擴充性和效能](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/A%20Case%20Study%20Using%20Replication%20to%20Build%20an%20Enterprise%20Ecosystem%20in%20Microsoft%20Dynamics%20ERP%20for%20Scalability%20and%20Performance.docx)Word 檔。  
  
  
