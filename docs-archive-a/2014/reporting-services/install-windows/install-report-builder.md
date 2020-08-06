---
title: 安裝獨立版本的報表產生器 (報表產生器) |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2ba8c132125f56ad833a71a1c82221e2bf28d13e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597632"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>安裝單機版報表產生器 (報表產生器)
  您可以從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=53613)的功能套件安裝報表產生器，或在已下載 ReportBuilder3_x86.msi （報表產生器的 Windows Installer 套件）的位置（例如公用資料夾）。  
  
 您也可以執行報表產生器的命令列安裝，並提供引數來自訂安裝。 除了標準的 MSI 內建參數以外，您還可以使用報表產生器所提供的自訂參數：RBINSTALLDIR 和 REPORTSERVERURL。 RBINSTALLDIR 會指定報表產生器的根安裝資料夾。 REPORTSERVERURL 會指定報表產生器用來在伺服器上儲存報表的預設報表伺服器。  
  
 如果您想要進行完全無訊息的安裝 (完全沒有使用者介面互動)，請指定 **/quiet** 選項。 根據設計，quiet 選項旗標會隱藏安裝錯誤。 因此，當您使用 quiet 選項時，建議您加入 **/l** 選項 (指定記錄)。  
  
> [!IMPORTANT]  
>  Windows Vista 和 Windows 7 安全性功能需要更高的權限才能執行命令列作業，並且會提示執行命令列的權限。 安裝不是無訊息的。 若要進行無訊息安裝，您必須以管理員的身分執行命令列。  
  
### <a name="to-install-report-builder-from-the-download-site"></a>若要從下載網站安裝報表產生器  
  
1.  移至[Microsoft SQL Server 2012 報表產生器](https://go.microsoft.com/fwlink/?LinkID=219138)，並找出網頁的 [報表產生器] 區段。  
  
2.  按一下 [ **X86 套件**]。  
  
3.  在 [檔案**下載**] 對話方塊中，按一下 [**執行**]。  
  
    > [!IMPORTANT]  
    >  僅從信任的來源下載檔案。  
  
4.  在 [Internet Explorer] 對話方塊中，按一下 [**執行**]。  
  
    > [!IMPORTANT]  
    >  僅從信任的來源執行檔案。  
  
5.  [Microsoft SQL Server 報表產生器精靈] 隨即啟動。  
  
6.  在 [**歡迎使用安裝精靈]** 頁面上，按 **[下一步]**。  
  
7.  閱讀 [**授權合約**] 頁面上的合約，然後選取 [**我接受授權合約中的條款**] 選項。 按 [下一步] 。  
  
8.  提供您的個人姓名和公司名稱。 按 [下一步] 。  
  
9. 在 [**特徵選取**] 頁面上，選擇性地按一下 **[流覽] 或 [** **磁片成本**]。 按 [下一步] 。  
  
    -   按一下 **[流覽]** 以查看報表產生器的預設位置，並加以更新。  
  
        > [!NOTE]  
        >  報表產生器的預設安裝資料夾為 \<drive> Program Files\Microsoft SQL Server。  
  
    -   按一下 [**磁片成本**] 以瞭解報表產生器使用多少磁碟空間。  
  
        > [!NOTE]  
        >  如果磁碟區沒有足夠的可用磁碟空間數量，該磁碟區就會反白顯示。  
  
10. 在 **[預設的目標伺服器]** 頁面上，選擇性地提供目標報表伺服器的 URL (如果它與預設值不同的話)。 按 [下一步] 。  
  
    > [!NOTE]  
    >  如果您計畫在報表產生器連接至報表伺服器時使用它，此時提供伺服器的 URL 比較方便。 不過，當您在報表產生器中工作時，也可以從 [**選項**] 對話方塊執行此動作。  
  
11. 按一下 [**安裝**]，完成報表產生器的安裝。  
  
### <a name="to-install-report-builder-from-a-share"></a>若要從共用位置安裝報表產生器  
  
1.  如需您在本機電腦上安裝報表產生器所執行之 ReportBuilder3_x86.msi.msi 的位置，請連絡系統管理員。  
  
2.  瀏覽並找出 ReportBuilder3_x86.msi.msi (報表產生器的 Windows 安裝程式套件 (MSI))，然後按一下此檔案。  
  
     [Microsoft SQL Server 報表產生器精靈] 隨即啟動。  
  
3.  在 [**歡迎使用安裝精靈]** 頁面上，按 **[下一步]**。  
  
4.  閱讀 [**授權合約**] 頁面上的合約，然後選取 [**我接受授權合約中的條款**] 選項。 按 [下一步] 。  
  
5.  提供您的個人姓名和公司名稱。 按 [下一步] 。  
  
6.  在 [**特徵選取**] 頁面上，選擇性地按一下 **[流覽] 或 [** **磁片成本**]。 按 [下一步] 。  
  
    -   按一下 **[流覽]** 以查看報表產生器的預設位置，並加以更新。  
  
        > [!NOTE]  
        >  報表產生器的預設安裝資料夾為 \<drive> Program Files\Microsoft SQL Server。  
  
    -   按一下 [**磁片成本**] 以瞭解報表產生器使用多少磁碟空間。  
  
        > [!NOTE]  
        >  如果磁碟區沒有足夠的可用磁碟空間數量，該磁碟區就會反白顯示。  
  
7.  在 **[預設的目標伺服器]** 頁面上，選擇性地提供目標報表伺服器的 URL (如果它與預設值不同的話)。 按 [下一步] 。  
  
    > [!NOTE]  
    >  如果您計畫在報表產生器連接至報表伺服器時使用它，此時提供伺服器的 URL 比較方便。 不過，當您在報表產生器中工作時，也可以從 [**選項**] 對話方塊執行此動作。  
  
8.  按一下 [**安裝**]，完成報表產生器的安裝。  
  
### <a name="to-install-report-builder-from-the-command-line"></a>若要從命令列安裝報表產生器  
  
1.  移至[Microsoft SQL Server 2012 報表產生器](https://go.microsoft.com/fwlink/?LinkID=219138)，並找出 [報表產生器] 區段。  
  
2.  按一下 [ **X86 套件**]。  
  
3.  按一下 [儲存]。  
  
4.  （選擇性）流覽至要儲存的位置，確認 [**另存**新檔] 選項是**Windows Installer 封裝**]，然後按一下 [**儲存**]。  
  
5.  在 **[開始]** 功能表上，按一下 **[執行]** 。  
  
6.  在 [開啟] 文字方塊中，輸入 `cmd.`  
  
7.  在 [命令提示字元] 視窗中，巡覽至儲存 ReportBuilder3_x86.msi 的資料夾。  
  
8.  輸入下列格式的命令：  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     安裝報表產生器的兩個專屬選項是：RBINSTALLDIR 和 REPORTSERVERURL。 您不需要在命令列中包含這兩個引數。 以下為基準命令：  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. 若要執行命令，請按 Enter 鍵。  
  
## <a name="see-also"></a>另請參閱  
 [安裝、卸載和報表產生器支援](../install-uninstall-and-report-builder-support.md)   
 [將獨立版本的報表產生器 &#40;報表產生器卸載&#41;](install-report-builder.md)  
  
  
