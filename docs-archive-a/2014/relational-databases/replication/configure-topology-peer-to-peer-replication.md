---
title: 設定拓撲 (點對點複寫) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.peers.f1
ms.assetid: 5377c59f-2e25-4852-a306-c87ae3dca9fd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2dfc09f5ae7f488afd46f29c301d11b7687e0a4b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585325"
---
# <a name="configure-topology-peer-to-peer-replication"></a>設定拓撲 (點對點複寫)
  您可以使用 **[設定拓撲]** 頁面來執行一些常見的組態設定工作，例如加入新的節點、刪除節點，以及在現有節點之間加入新連接。 您在此精靈之 **[發行集]** 頁面上選取的節點會顯示在設計介面上。 若要指定組態選項，請以滑鼠右鍵按一下節點、連接或設計介面。

> [!NOTE]
>  「設定點對點拓撲精靈」會在關閉精靈時要求拓撲資訊。 如果您在所有節點回應資訊要求之前關閉並重新開啟此精靈，精靈可能會顯示部分網路。

## <a name="options"></a>選項。
 **[設定拓撲]** 頁面包含當您以滑鼠右鍵按一下元素時可用的介面元素和選項。 下表描述的是每個介面元素。

|介面元素|描述|
|-----------------------|-----------------|
|設計介面|顯示其他介面元素。 若要加入元素，請以滑鼠右鍵按一下設計介面。|
|![拓撲中的第一個節點](media/p2pwizard-firstnode.gif "拓撲中的第一個節點")|拓撲中的原始節點。 系統會使用原始節點的發行集資料庫副本來初始化新的節點。|
|![我們有完整資訊](media/p2pwizard-complete.gif "我們擁有其完整資訊的節點")或更新版本的節點，複寫具有完整的資訊。 若要指定組態選項，請以滑鼠右鍵按一下節點。|
|![我們沒有其完整資訊的節點](media/p2pwizard-incomplete.gif "我們沒有其完整資訊的節點")|複寫具有不完整資訊的節點。 若要指定組態選項，請以滑鼠右鍵按一下節點。 由於下列其中一項原因，所以複寫具有不完整的資訊：<br /><br /> 節點正在執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體 (無法儲存精靈所需的所有中繼資料)。<br /><br /> 節點正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新版本，但是複寫無法從節點中擷取訂閱資訊。 若要疑難排解這個情況：<br />-請確定節點上的資料庫在線上，而且您可以使用與連接到該節點的散發代理程式相同的認證來連接它。<br />-確定連接到節點的記錄讀取器代理程式和所有散發代理程式都在執行中。<br />-請確定 [重新整理超時] 已設定為 [夠高]，以收集所有拓撲資訊。 若要設定逾時，請以滑鼠右鍵按一下設計介面，然後按一下 **[設定重新整理逾時]**。|
|含有箭頭的灰線|兩個節點之間的連接。 若要加入連接，請以滑鼠右鍵按一下您想要連接的其中一個節點。 若要移除連接，請以滑鼠右鍵按一下該連接。<br /><br /> 如果此線條只有單一箭頭，就表示複寫具有其中一個節點的不完整資訊。|

### <a name="options-for-the-design-surface"></a>設計介面的選項
 **重繪圖形**在設計介面上重新繪製物件，而不重新整理拓撲。 重繪可能會提供較佳的拓撲檢視。

 重新整理**拓撲**查詢拓撲中的每個節點，並顯示每個節點的更新資訊。 如果節點很多，這個處理序可能需要幾分鐘。

 如果精靈要求拓撲資訊，然後您在所有節點回應要求之前關閉精靈並重新開啟，這個頁面可能會無法顯示拓撲中的所有節點。

 **加入新的對等節點**將的實例加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 至點對點拓撲。 如果您加入執行個體當做節點，系統會在精靈完成之後，於該執行個體上建立發行集。 在您加入節點之後，請以滑鼠右鍵按一下它，以便在新節點與現有節點之間加入連接。

 若要參與點對點拓撲，這個執行個體必須符合下列需求：

-   它必須已經設定為散發者或與遠端散發者產生關聯。

-   它必須包含涉及複寫之資料庫的副本。 這個副本通常是原始發行集資料庫的還原備份。

 **選取節點 (s) 以查看**選取要在設計介面上查看的節點。 如果拓撲具有大量節點，這個選項就很有用。 請注意，您只能在設計介面上顯示的節點之間加入連接。

 **設定**重新整理超時指定在作業超時之前，重新整理程式可以執行的時間長度。

### <a name="options-for-each-node"></a>每個節點的選項
 **加入新的對等連接**在兩個節點之間新增連接。 例如，如果您在節點 A 與節點 B 之間加入連接，複寫就會加入兩個訂閱：第一個訂閱可讓節點 A 收到位於節點 B 之發行集的變更，而第二個訂閱可讓節點 B 收到位於節點 A 之發行集的變更。

 **刪除對等節點**從拓撲中移除節點。 例如，如果您移除節點 C，就會一併移除位於該節點的發行集。 此外，系統也會移除節點 A 與節點 C 之間的訂閱，以及節點 B 與節點 C 之間的訂閱。 但是，系統不會刪除位於節點 C 的資料庫，而且不會停用發行和散發功能。

> [!NOTE]
>  當您設定點對點複寫時，會為每個節點指定一個識別碼。 此識別碼在拓撲的所有節點中必須是唯一的，並會儲存在 [MSpeer_originatorid_history](/sql/relational-databases/system-tables/mspeer-originatorid-history-transact-sql) 系統資料表的 originator_id 資料行中。 如果從拓撲中移除某個節點，其識別碼仍然會保留在記錄資料表中。 如果已移除的節點中有仍然在拓撲中進行複寫的變更，保留識別碼可防止發生假衝突。 如果您要針對新節點重複使用識別碼，必須先從所有節點的 MSpeer_originatorid_history 資料表中手動刪除該識別碼。 在您刪除節點的識別碼前，執行 [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) 以確認已複寫源自該節點的所有變更。

 **連接到所有顯示的節點**在選取的節點與其他所有節點之間新增連接。 例如，如果您在三節點拓撲中，針對節點 C 選取此選項，複寫就會加入四個訂閱：其中兩個訂閱可讓節點 A 和節點 B 收到位於節點 C 之發行集的變更，而另外兩個訂閱可讓節點 C 收到位於節點 A 和節點 B 之發行集的變更。

 **選取節點 (s) 以查看**選取要在設計介面上查看的節點。 如果拓撲具有大量節點，這個選項就很有用。 請注意，您只能在設計介面上顯示的節點之間加入連接。

### <a name="options-for-the-connection-arrows"></a>連接箭頭的選項
 **移除對等連接**移除兩個節點之間的連接。 例如，如果您移除節點 A 與節點 B 之間的連接，複寫就會卸除兩個訂閱：可讓節點 A 收到位於節點 B 之發行集的變更的訂閱，以及可讓節點 B 收到位於節點 A 之發行集的變更的訂閱。

## <a name="see-also"></a>另請參閱
 [設定發佈和散發](configure-publishing-and-distribution.md)[管理點對點拓朴 &#40;複寫 transact-sql 程式設計&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md) [點對點異動複寫](transactional/peer-to-peer-transactional-replication.md)


