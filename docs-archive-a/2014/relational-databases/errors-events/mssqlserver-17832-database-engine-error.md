---
title: MSSQLSERVER_17832 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17828 (Database Engine error)
- maxtokensize
- 17832 (Database Engine error)
- login packet (bad)
ms.assetid: bd56ffe4-0855-4ada-8aca-251fbc6ff2ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dba214e2cce04ff2583e12ae7cee9b54373390a6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687945"
---
# <a name="mssqlserver_17832"></a>MSSQLSERVER_17832
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|17832|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SRV_BAD_LOGIN_PKT|  
|訊息文字|用來開啟連接的登入封包的結構無效; 此連接已經關閉。 請聯繫用戶端程式庫的供應商。%.*ls|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦無法處理用戶端登入封包。 這可能是因為封包的建立方式不正確，或者封包在傳輸期間已損毀。 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的組態也可能會造成這個錯誤。 所列出的 IP 位址就是用戶端電腦的位址。  
  
### <a name="more-information"></a>相關資訊  
 在 Kerberos 環境中使用 Windows 驗證時，用戶端就會接收包含專用權屬性憑證 (PAC) 的 Kerberos Ticket。 此 PAC 包含各種類型的授權資料，包括使用者為所屬成員的群組、使用者擁有的權限，以及哪些原則會套用至使用者。 當此用戶端接收 Kerberos Ticket 時，PAC 中所包含的資訊就會用來產生使用者的存取 Token。 此用戶端會將 Token 呈現給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦，當做登入封包的一部分。  
  
 如果此 Token 的建立方式不正確或者在傳輸期間已損毀，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就無法提供有關問題的其他資訊。  
  
 當使用者是屬於許多群組的成員或者具有許多原則時，此 Token 的大小可能會超過一般大小才能列出所有項目。 如果此 Token 的大小超過伺服器電腦的 **MaxTokenSize** 值，用戶端就會因為一般網路錯誤 (GNE) 而無法連線，而且可能會發生錯誤 17832。 這個問題可能只會影響某些使用者：具有許多群組或原則的使用者。 當此問題是伺服器電腦的 **MaxTokenSize** 值時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中的錯誤 17832 將會伴隨狀態 9 的錯誤一起出現。 如需 Kerberos 和 **MaxTokenSize** 的其他詳細資料，請參閱 [KB327825](https://support.microsoft.com/kb/327825)。  
  
## <a name="user-action"></a>使用者動作  
 若要解決這個問題，請將伺服器電腦的 **MaxTokenSize** 值增加到足以包含組織內任何使用者之最大 Token 的大小。 若要針對組織研究正確的 Token 大小，請考慮使用 **Tokensz** 應用程式。   
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 **變更伺服器電腦上的 MaxTokenSize**  
  
1.  在 **[開始]** 功能表上，按一下 **[執行]** 。  
  
2.  輸入 `regedit` ，然後按一下 **[確定]**。 (如果出現 [使用者帳戶控制] 對話方塊，請按一下 [繼續])。  
  
3.  巡覽至 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\Kerberos\Parameters**。  
  
4.  如果 **MaxTokenSize** 參數不存在，請以滑鼠右鍵按一下 [參數]，並指向 [新增]，然後按一下 [DWORD (32-位元) 值]。 將此登錄項目命名為 **MaxTokenSize**。  
  
5.  以滑鼠右鍵按一下 **MaxTokenSize**，然後按一下 [修改]。  
  
6.  在 [數值資料] 方塊中，輸入所需的 **MaxTokenSize** 值。  
  
    > [!NOTE]  
    >  十六進位值 ffff (十進位值 65535) 是最大的建議 Token 大小。 雖然提供這個值可能會解決此問題，但是卻可能會對效能造成整部電腦的不良影響。 我們建議您建立允許組織內任何使用者之最大 Token 的最小 **MaxTokenSize** 值並且輸入該值。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  關閉 [登錄編輯程式]。  
  
9. 重新啟動電腦。  
  
  
