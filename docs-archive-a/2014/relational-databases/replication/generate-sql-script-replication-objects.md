---
title: 產生 SQL 指令碼 (複寫物件) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 31a4b318eb3a4c0e5d9f79f43efdcf97c42957f9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585833"
---
# <a name="generate-sql-script-replication-objects"></a>產生 SQL 指令碼 (複寫物件)
  複寫指令碼包含要實作已編寫複寫元件之指令碼所必要的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系統預存程序，例如發行集或訂閱。 拓撲中的所有複寫元件都應作為損毀復原計畫的一部份來編寫指令碼，而指令碼也可以用於自動執行重複性工作。 複寫提供編寫複寫物件之指令碼的兩個對話方塊：  
  
-   [產生 SQL 指令碼]，這可從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中 [複寫] 資料夾和所有子資料夾的操作功能表中使用。 此對話方塊可讓您撰寫 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上所有複寫物件的指令碼。  
  
-   [產生 SQL 指令碼 \<ObjectName>]，這可從發行集和訂閱的操作功能表使用。 此對話方塊可讓您編寫個別物件的指令碼。  
  
 這些對話方塊會編寫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]單一執行個體上之物件的指令碼；它們不會連接到其他執行個體來編寫相關物件的指令碼。  
  
## <a name="generate-sql-script-options"></a>產生 SQL 指令碼選項  
 **散發者屬性**  
 選取即可編寫預存程序的指令碼以：啟用或停用散發者；加入或卸除與散發者相關聯的發行者；以及建立或卸除散發資料庫。  
  
 **下列資料來源中的發行集**  
 選取即可編寫預存程序的指令碼以：啟用或停用發行；建立或卸除發行集、發行項、發送訂閱以及複寫作業。  
  
 **下列資料來源中的訂閱**  
 選取即可編寫預存程序的指令碼，以建立或卸除提取訂閱與複寫作業。  
  
 **[若要建立或啟用元件]** 與 **[若要卸除或停用元件]**  
 指定指令碼是否應包含建立或卸除複寫物件的命令。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您使用對話方塊來建立一組啟用和停用元件的指令碼。  
  
 **複寫作業**  
 選取即可編寫複寫作業的指令碼，但預存程序呼叫除外。 只有從散發者編寫指令碼時，才能使用此選項。  
  
 複寫預存程序會在執行時建立必要的作業，因此不需要選取此選項。 不過，保留建立作業的記錄，在萬一必須重新建立個別作業時非常有用。  
  
## <a name="generate-sql-script-objectname-options"></a>產生 SQL 指令碼 \<ObjectName> 選項  
 **[若要建立或啟用元件]** 與 **[若要卸除或停用元件]**  
 指定指令碼是否應包含建立或卸除複寫物件的命令。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您使用對話方塊來建立一組啟用和停用元件的指令碼。  
  
 **複寫作業**  
 只能從 **[產生 SQL 指令碼]** 對話方塊使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [編寫複寫指令碼](scripting-replication.md)  
  
  
