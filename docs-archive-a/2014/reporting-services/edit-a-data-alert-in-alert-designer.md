---
title: 在警示設計工具中編輯資料警示 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- editing, data alerts
- updating, data alerts
- editing, alerts
- updating, alerts
ms.assetid: dde3664d-90b5-4b12-969e-39152c86e58a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9906b33ae50d51733eaec1bf5c201c9f5b5d120e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703902"
---
# <a name="edit-a-data-alert-in-alert-designer"></a>在警示設計工具中編輯資料警示
  從 [資料警示管理員] 開啟您要編輯的資料警示定義。 只有建立警示定義的使用者才能進行編輯。 如需開啟資料警示管理員的詳細資訊，請參閱 [在資料警示管理員中管理我的資料警示](manage-my-data-alerts-in-data-alert-manager.md)。

 下圖說明 [資料警示管理員] 中資料警示的內容功能表。

 ![按一下 [編輯] 來開啟資料警示設計工具](media/rs-alertmanageriwopendesigner.gif "按一下 [編輯] 來開啟資料警示設計工具")

 下列程序包括從 [資料警示管理員] 開啟警示定義，以便在 [資料警示設計工具] 中進行編輯的步驟。

### <a name="to-edit-a-data-alert-definition-in-data-alert-designer"></a>在資料警示設計工具中編輯資料警示定義

1.  在 [資料警示管理員] 中，以滑鼠右鍵按一下您要編輯的資料警示定義，然後按一下 [編輯]****。

     警示定義會在 [資料警示設計工具] 中開啟。

2.  請更新規則、排程設定和電子郵件設定。 如需詳細資訊，請參閱 [資料警示設計工具](../../2014/reporting-services/data-alert-designer.md) 和 [在資料警示設計工具中建立資料警示](create-a-data-alert-in-data-alert-designer.md)。

    > [!NOTE]
    >  您無法選擇不同的資料摘要。 若要使用不同的資料摘要，您必須建立新的資料警示定義。

3.  按一下 [儲存]。

    > [!NOTE]
    >  如果報表已變更，而且從報表產生的資料摘要也已變更，則警示定義可能已無效。 當警示定義參考其規則的資料行已從報表中刪除或變更資料類型，或是報表已刪除或移動時，就會發生這種情形。 您可以開啟無效的警示定義，但是無法重新儲存它，除非依據建立定義的目前版本報表資料摘要成為有效的警示定義。 若要深入了解如何從多個報表產生資料摘要，請參閱[從多個報表產生資料摘要 &#40;報表產生器及 SSRS&#41;](report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)。

## <a name="see-also"></a>另請參閱
 警示系統管理員[Reporting Services 資料警示](../ssms/agent/alerts.md)[的資料警示管理員](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)


