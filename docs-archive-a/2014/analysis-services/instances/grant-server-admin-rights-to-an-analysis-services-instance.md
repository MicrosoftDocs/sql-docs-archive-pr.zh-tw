---
title: 授與伺服器管理員許可權 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
author: minewiskan
ms.author: owend
ms.openlocfilehash: 822227ae89f4f219a055bcc0d6d6b0a228f7964b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700474"
---
# <a name="grant-server-administrator-permissions-analysis-services"></a>授與伺服器管理員權限 (Analysis Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體內伺服器管理員角色的成員對於該執行個體中的所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件和資料具有不受限制的存取權。 使用者必須是伺服器管理員角色的成員，才能執行整個伺服器範圍的工作，例如建立資料庫或處理資料庫、修改伺服器屬性或啟動追蹤 (但處理事件不算)。

 在安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 時，會建立角色成員資格。 在提供伺服器時，執行安裝程式的使用者可將本身加入角色或加入其他使用者。 您可以使用下列程序，以後續安裝工作的形式修改角色成員資格。

## <a name="modify-server-role-membership"></a>修改伺服器角色成員資格

1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，然後以滑鼠右鍵按一下物件總管中的執行個體名稱，再按一下 [屬性]****。

2.  按一下 **[選取頁面]** 窗格中的 **[安全性]** ，然後按一下頁面底部的 **[加入]** ，以將一個或多個 Windows 使用者或群組加入至伺服器角色。

     ![Management Studio 中的 [加入使用者] 對話方塊](../media/ssas-serveradminadd.png "Management Studio 中的 [加入使用者] 對話方塊")

 在安裝期間，SQL Server 安裝程式會要求您至少指定一個使用者帳戶做為 Analysis Services 系統管理員。

 依預設，也會將 Analysis Server 的管理權限授與本機 Administrators 群組的成員。 雖然本機群組未明確授與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器管理員角色的成員資格，但本機管理員可以建立資料庫，新增使用者和權限，以及執行系統管理員可執行的其他工作。 這個行為是可設定的， 它是由 `BuiltinAdminsAreServerAdmins` 伺服器屬性所決定，預設會設定為**true** 。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中變更這個屬性。 如需詳細資訊，請參閱 [Security Properties](../server-properties/security-properties.md)。

 您也可以使用分析管理物件 (AMO) 來管理伺服器角色。 如需詳細資訊，請參閱[使用分析管理物件 &#40;AMO&#41; 來開發](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)。

## <a name="see-also"></a>另請參閱
 [&#40;Analysis Services&#41;安全性角色來授權物件和作業的存取權](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md) [&#40;Analysis Services 多維度資料&#41;](../multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)


