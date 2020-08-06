---
title: AlwaysOn 可用性群組 (SQL Server) 的 Transact-sql 語句總覽 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: 184d0a81-2259-4db9-9d0d-01aac0b502c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ff25fecf54cfdd1d9c03d1586f0272896542bfa7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708646"
---
# <a name="overview-of-transact-sql-statements-for-alwayson-availability-groups-sql-server"></a>AlwaysOn 可用性群組的 Transact-SQL 陳述式概觀 (SQL Server)
  本主題介紹支援部署 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 以及建立及管理給定可用性群組、可用性複本及可用性資料庫的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 陳述式。  
  
  
##  <a name="create-endpoint"></a><a name="CreateEndpoint"></a>建立端點  
 [建立端點 .。。若為 DATABASE_MIRRORING](/sql/t-sql/statements/create-endpoint-transact-sql)則會建立資料庫鏡像端點（如果伺服器實例上沒有）。 您要部署 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 或資料庫鏡像的每個伺服器執行個體都需要一個資料庫鏡像端點。  
  
 在您要建立端點的伺服器執行個體上執行此陳述式。 每個給定的伺服器執行個體上只能建立一個資料庫鏡像端點。 如需詳細資訊，請參閱 [資料庫鏡像端點 &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)。  
  
##  <a name="create-availability-group"></a><a name="CreateAG"></a>建立可用性群組  
 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql) 會建立新的可用性群組並選擇性地建立可用性群組接聽程式。 您至少必須指定本機伺服器執行個體，這會成為初始主要複本。 您最多也可以選擇指定四個次要複本。  
  
 在您要裝載新可用性群組之初始主要複本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上執行 CREATE AVAILABILITY GROUP。 這個伺服器實例必須位於 Windows Server 容錯移轉叢集的節點 (WSFC)  (如需詳細資訊，請參閱[AlwaysOn 可用性群組 &#40;SQL Server&#41;的必要條件、限制和建議](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
##  <a name="alter-availability-group"></a><a name="AlterAG"></a>ALTER AVAILABILITY GROUP  
 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 支援變更現有的可用性群組或可用性群組接聽程式，並支援可用性群組容錯移轉。  
  
 在裝載目前主要複本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上執行 ALTER AVAILABILITY GROUP。  
  
##  <a name="alter-database--set-hadr-"></a><a name="AlterDb"></a>ALTER DATABASE .。。設定 HADR .。。  
 ALTER DATABASE 陳述式中 [SET HADR](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) 子句的選項可讓您將次要資料庫聯結至對應主要資料庫的可用性群組、移除聯結的資料庫、在聯結的資料庫上暫停資料同步處理，以及繼續資料同步處理。  
  
##  <a name="drop-availability-group"></a><a name="DropAG"></a>捨棄可用性群組  
 [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) 可移除指定的可用性群組及其所有複本。 DROP AVAILABILITY GROUP 可從 WSFC 容錯移轉叢集中的任何 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 節點執行。  
  
##  <a name="restrictions-on-the-availability-group-transact-sql-statements"></a><a name="Restrictions"></a>可用性群組 Transact-sql 語句的限制  
 CREATE AVAILABILITY GROUP、ALTER AVAILABILITY GROUP 及 DROP AVAILABILITY GROUP [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式具有下列限制：  
  
-   除了 DROP AVAILABILITY GROUP 之外，執行這些陳述式需要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上啟用 HADR 服務。 如需詳細資訊，請參閱[啟用和停用 AlwaysOn 可用性群組 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)。  
  
-   您無法在交易或批次內執行這些陳述式。  
  
-   這些陳述式雖然在失敗後會盡最大努力清理，但是不保證可回復失敗時的所有變更。 不過，系統應該能夠乾淨地處理，再忽略部分失敗。  
  
-   這些陳述式不支援運算式或變數。  
  
-   如果在其他可用性群組動作或復原進行時執行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，陳述式會傳回錯誤。 請等候動作或復原完成，再視需要重試陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
