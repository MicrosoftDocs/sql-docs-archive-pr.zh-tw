---
title: 將資料採礦解決方案部署到舊版的 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [Analysis Services]
- holdout [data mining]
- deploy [Analysis Services]
- time series [Analysis Services]
- deploying [Analysis Services - data mining]
- synchronization [Analysis Services]
- deployment [Analysis Services]
ms.assetid: 2715c245-f206-43af-8bf5-e6bd2585477a
author: minewiskan
ms.author: owend
ms.openlocfilehash: f09a37c078cf58f24db9a08e3ddcb68cb2638717
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599268"
---
# <a name="deploy-a-data-mining-solution-to-previous-versions-of-sql-server"></a>將資料採礦方案部署到舊版的 SQL Server
  本章節描述當您嘗試將 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 執行個體內建立的資料採礦模型或資料採礦結構部署到使用 SQL Server 2005 Analysis Services 的資料庫，或是當您將 SQL Server 2005 中建立的模型部署到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體時，可能發生的相容性問題。  
  
 不支援部署到 SQL Server 2000 Analysis Services 的執行個體。  
  
 [部署時間序列模型](#bkmk_TimeSeries)  
  
 [部署含鑑效組的模型](#bkmk_Holdout)  
  
 [部署含篩選的模型](#bkmk_Filter)  
  
 [從資料庫備份還原](#bkmk_Backup)  
  
 [使用資料庫同步處理](#bkmk_Synch)  
  
##  <a name="deploying-times-series-models"></a><a name="bkmk_TimeSeries"></a>部署時間序列模型  
 Microsoft 時間序列演算法在 SQL Server 2008 中增強了功能，其方式是加入第二個補充性的演算法 ARIMA。 如需時間序列演算法變更的詳細資訊，請參閱 [Microsoft 時間序列演算法](microsoft-time-series-algorithm.md)。  
  
 因此，使用新 ARIMA 演算法的時間序列採礦模型的行為可能與部署到 SQL Server 2005 Analysis Services 執行個體時不同。  
  
 如果您已明確設定 PREDICTION_SMOOTHING 參數來控制預測中 ARTXP 和 ARIMA 模型的混用，當您將此模型部署到 SQL Server 2005 執行個體時，Analysis Services 將會引發錯誤，指出此參數無效。 若要避免此錯誤，您必須刪除 PREDICTION_SMOOTHING 參數，並將模型轉換成純正的 ARTXP 模型。  
  
 相反地，如果您要將使用 SQL Server 2005 Analysis Services 建立的時間序列模型部署到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體，當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟此採礦模型時，定義檔案會先轉換成新的格式，而且預設會將兩個新的參數加入到所有時間序列模型。 加入的 FORECAST_METHOD 參數具有預設值 MIXED，而且加入的 PREDICTION_SMOOTHING 參數具有預設值 0.5。 但是，此模型將繼續只使用 ARTXP 進行預測，直到重新處理此模型為止。 一旦您重新處理此模型之後，預測就會變更為使用 ARIMA 和 ARTXP 這兩者。  
  
 因此，如果您要避免變更模型，應該只瀏覽模型，而絕對不要處理它。 另外，您也可以明確設定 FORECAST_METHOD 或 PREDICTION_SMOOTHING 參數。  
  
 如需設定混合模型的詳細資訊，請參閱 [Microsoft 時間序列演算法技術參考](microsoft-time-series-algorithm-technical-reference.md)。  
  
 如果用於模型資料來源的提供者是 SQL Client Data Provider 10，您也必須修改資料來源定義來指定舊版的 SQL Server Native Client。 否則， [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 會產生錯誤，指出此提供者尚未註冊。  
  
##  <a name="deploying-models-with-holdout"></a><a name="bkmk_Holdout"></a>使用維持的部署模型  
 如果您使用 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 來建立包含用於測試資料採礦模型之鑑效組資料分割的採礦結構，此採礦結構可以部署到 SQL Server 2005 執行個體，但是資料分割資訊將會遺失。  
  
 當您在 SQL Server 2005 Analysis Services 中開啟此採礦結構時， [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 會引發錯誤，然後重新產生此結構來移除鑑效組資料分割。  
  
 重建結構之後，屬性視窗中無法再使用維持的分割區大小。不過，值 \<ddl100_100:HoldoutMaxPercent> 30 \</ddl100_100:HoldoutMaxPercent>) 可能仍存在於 ASSL 腳本檔案中。  
  
##  <a name="deploying-models-with-filters"></a><a name="bkmk_Filter"></a>使用篩選部署模型  
 如果您使用 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 將篩選套用到採礦模型，此模型可以部署到 SQL Server 2005 執行個體，但是篩選將不會套用。  
  
 當您開啟此採礦模型時， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會引發錯誤，然後重新產生此模型來移除篩選。  
  
##  <a name="restoring-from-database-backups"></a><a name="bkmk_Backup"></a>從資料庫備份還原  
 您無法將 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中建立的資料庫備份還原到 SQL Server 2005 執行個體。 如果您這樣做，SQL Server Management Studio 會產生錯誤。  
  
 如果您建立 SQL Server 2005 Analysis Services 資料庫的備份，並將此備份還原到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體，則所有時間序列模型都會修改，如上節所述。  
  
##  <a name="using-database-synchronization"></a><a name="bkmk_Synch"></a>使用資料庫同步處理  
 不支援從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 到 SQL Server 2005 的資料庫同步處理。  
  
 如果您嘗試同步處理 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫，伺服器會傳回錯誤，而且資料庫同步處理會失敗。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 回溯相容性](../analysis-services-backward-compatibility.md)  
  
  
