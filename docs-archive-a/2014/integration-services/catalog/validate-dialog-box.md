---
title: 驗證對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackagevalidate.f1
- sql12.ssis.ssms.isprojectvalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 69e29d106dc9f4f100bf191911c5c34e0250be8f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592175"
---
# <a name="validate-dialog-box"></a>驗證對話方塊
  使用 **[驗證]** 對話方塊檢查 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案或封裝中的常見問題。  
  
 如果有問題，就會在對話方塊上方顯示一個訊息。 否則，「就緒」這個詞會顯示在上方。  
  
 **您想要做什麼事？**  
  
-   [開啟 [驗證] 對話方塊](#open_dialog)  
  
-   [設定 [一般] 頁面上的選項](#general)  
  
##  <a name="open-the-validate-dialog-box"></a><a name="open_dialog"></a> 開啟 [驗證] 對話方塊  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
     您正在連線到裝載 SSISDB 資料庫的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[SSISDB]** 節點。  
  
4.  展開包含您要驗證之專案或封裝的資料夾。  
  
5.  以滑鼠右鍵按一下封裝，然後按一下 [驗證]  。  
  
##  <a name="set-the-options-on-the-general-page"></a><a name="general"></a> 設定 [一般] 頁面上的選項  
 **環境**  
 選取您要用來驗證專案或封裝的環境。  
  
 **32 位元執行階段**  
 選擇使用 32 位元執行階段執行封裝。  
  
 **[參數]** 索引標籤會列出您用來驗證專案或封裝的參數值。 以下是在 [參數] 索引標籤上的選項。  
  
 **容器**  
 列出包含參數的物件。  
  
 **參數**  
 列出參數的名稱  
  
 **ReplTest1**  
 列出參數值。  
  
 **[連接管理員]** 索引標籤會列出您用來驗證專案或封裝的連接管理員屬性值。  
  
 以下是在 **[連接管理員]** 索引標籤上的選項。  
  
 **容器**  
 列出包含連接管理員的物件。  
  
 **名稱**  
 列出連接管理員名稱。  
  
 **屬性名稱**  
 列出連接管理員屬性的名稱。  
  
 **ReplTest1**  
 列出指派給連接管理員屬性的值。  
  
  
