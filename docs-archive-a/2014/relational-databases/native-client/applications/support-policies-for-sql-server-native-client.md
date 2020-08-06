---
title: SQL Server Native Client 的支援原則 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 09c80cf4-23e6-4027-a24f-cdb9c87af811
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e2ace1756705d6a1cb08b0701d3bf79b5cb96ce
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706402"
---
# <a name="support-policies-for-sql-server-native-client"></a>SQL Server Native Client 的支援原則
  本主題討論如何搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用各種不同的資料存取元件。  
  
## <a name="server-support"></a>伺服器支援  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 支援與 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]、[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]的連接。  
  
## <a name="supported-operating-system-versions"></a>支援的作業系統版本  
 下表將列出哪些作業系統支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
|SQL Server Native Client 版本|支援的作業系統|  
|--------------------------------------|---------------------------------|  
|SQL Server Native Client (SQL Server 2005)|-Microsoft Windows 2000 Service Pack 4 或更新版本<br />-Microsoft Windows Server 2003 或更新版本<br />-Microsoft Windows XP Service Pack 1 或更新版本<br />-Microsoft Windows Vista (需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 2 或更新版本) <br />-Microsoft Windows Server 2008 (需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 2 或更新版本) |  
|SQL Server Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) |-Microsoft Windows Server 2003 Service Pack 2 或更新版本<br />-Microsoft Windows XP Service Pack 2 或更新版本<br />-Microsoft Windows Vista<br />-Microsoft Windows Server 2008|  
|SQL Server Native Client 10.5 ([!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]) |-Microsoft Windows Server 2003 Service Pack 2 或更新版本<br />-Microsoft Windows XP Service Pack 2 或更新版本<br />-Microsoft Windows Vista<br />-Microsoft Windows Server 2008<br />-Microsoft Windows 7|  
|SQL Server Native Client 11.0 ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])|-Microsoft Windows Vista<br />-Microsoft Windows Server 2008<br />-Microsoft Windows 7<br />-Microsoft Windows 8<br />-Microsoft Windows Server 2012|  
  
## <a name="ado-support-policies"></a>ADO 支援原則  
 如果 ADO 應用程式不需要 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的任何功能，就可以使用 Windows 隨附的 SQLOLEDB OLE DB 提供者。  
  
 ADO 應用程式可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含在中的 Native Client 版本 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 。 ADO 應用程式也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 (隨附於 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])，但是如果它們這樣做，就必須在連接字串中指定 `DataTypeCompatibility=80`。 當連接字串中存在 `DataTypeCompatibility=80` 時，只能使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的功能。  
  
## <a name="bcp-support-policies"></a>BCP 支援原則  
 從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始，bcp.exe 便支援不超過提供 bcp.exe 之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本前三個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本的資料檔案。  
  
## <a name="odbc-support-policies"></a>ODBC 支援原則  
 應用程式應該使用 Windows 作業系統隨附的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC 驅動程式。 如果應用程式經認證可搭配特定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 版本使用，您就可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式。  
  
## <a name="ole-db-support-policies"></a>OLE DB 支援原則  
 應用程式應該使用 Windows 作業系統隨附的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 提供者。 如果應用程式經認證可搭配特定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 版本使用，您就可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者。  
  
 如果未經認證可搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用的 OLE DB 應用程式在其連接字串中指定了 `DataTypeCompatibility=80`，它們就可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
 如果使用 OLE DB 服務元件的 OLE DB 應用程式在其連接字串中指定了 `DataTypeCompatibility=80`，它們就只能使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 不過， [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 在此情況下，將無法使用之後新增的任何功能。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建置應用程式](building-applications-with-sql-server-native-client.md)  
  
  
