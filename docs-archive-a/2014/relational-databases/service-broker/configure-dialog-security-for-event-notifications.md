---
title: 設定事件通知的對話安全性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d83bfe63c3a9b24c2be8d08916dd2384c59edc93
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598777"
---
# <a name="configure-dialog-security-for-event-notifications"></a>設定事件通知的對話安全性
  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話安全性。 對話方塊安全性必須根據 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話方塊完整安全性模型來手動設定。 完整安全性模型使傳送到遠端伺服器和自遠端伺服器傳送的訊息得以加密和解密。 雖然事件通知是以單一方向傳送，但也會以相反方向傳回其他訊息 (例如錯誤)。  
  
## <a name="configuring-dialog-security-for-event-notifications"></a>設定事件通知的對話方塊安全性  
 下列步驟描述實作事件通知對話方塊安全性所需的程序。 這些步驟包括要對來源伺服器和目標伺服器採取的動作。 來源伺服器就是建立事件通知的伺服器。 目標伺服器是接收事件通知訊息的伺服器。 在繼續下一步之前，您必須為來源伺服器和目標伺服器完成每一個步驟的動作。  
  
> [!IMPORTANT]  
>  您必須以有效起始日和到期日建立所有憑證。  
  
 **步驟 1：建立 TCP 通訊埠編號和目標服務名稱。**  
  
 建立來源伺服器和目標伺服器將接收訊息的 TCP 通訊埠。 您也必須決定目標服務的名稱。  
  
 **步驟 2：為資料庫層級驗證設定加密和憑證共用。**  
  
 在來源和目標伺服器上完成下列動作。  
  
|來源伺服器|目標伺服器|  
|-------------------|-------------------|  
|選擇或建立資料庫來保存事件通知和主要金鑰。|選擇或建立資料庫來保存主要金鑰。|  
|如果來源資料庫沒有主要金鑰，請 [建立主要金鑰](/sql/t-sql/statements/create-master-key-transact-sql)。 來源和目標資料庫上必須有主要金鑰才能協助保護其個別憑證。|如果目標資料庫沒有主要金鑰，請建立主要金鑰。|  
|為來源資料庫[建立登入](/sql/t-sql/statements/create-login-transact-sql) 和對應的 [使用者](/sql/t-sql/statements/create-user-transact-sql)。|為目標資料庫建立登入和對應的使用者。|  
|[建立憑證](/sql/t-sql/statements/create-certificate-transact-sql) ，這是來源資料庫的使用者所擁有的憑證。|建立憑證，這是目標資料庫的使用者所擁有的憑證。|  
|[備份憑證](/sql/t-sql/statements/backup-certificate-transact-sql) 到可供目標伺服器存取的檔案。|備份憑證到可供來源伺服器存取的檔案。|  
|[建立使用者](/sql/t-sql/statements/create-user-transact-sql)時，指定目標資料庫的使用者和 WITHOUT LOGIN。 此使用者將擁有要從備份檔案建立的目標資料庫憑證。 使用者不必對應到登入，因為此使用者唯一的目的是要擁有接下來的步驟 3 所建立的目標資料庫憑證。|建立使用者時，指定來源資料庫的使用者和 WITHOUT LOGIN。 此使用者將擁有要從備份檔案建立的來源資料庫憑證。 使用者不必對應到登入，因為此使用者唯一的目的是要擁有接下來的步驟 3 所建立的來源資料庫憑證。|  
  
 **步驟 3：為資料庫層級驗證共用憑證和授與權限。**  
  
 在來源和目標伺服器上完成下列動作。  
  
|來源伺服器|目標伺服器|  
|-------------------|-------------------|  
|從目標憑證的備份檔案[建立憑證](/sql/t-sql/statements/create-certificate-transact-sql) 時，指定目標資料庫使用者作為擁有者。|從來源憑證的備份檔案建立憑證時，指定來源資料庫使用者作為擁有者。|  
|[授與權限](/sql/t-sql/statements/grant-transact-sql) 來建立來源資料庫使用者的事件通知。 如需此權限的詳細資訊，請參閱 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-notification-transact-sql)。|授與 REFERENCES 權限給現有的事件通知 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 合約上的目標資料庫使用者： `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`。|  
|[建立遠端服務繫結](/sql/t-sql/statements/create-remote-service-binding-transact-sql) 至目標服務，並指定目標資料庫使用者的認證。 遠端服務繫結保證來源資料庫使用者擁有之憑證中的公開金鑰會驗證傳送至目標伺服器的訊息。|[授與](/sql/t-sql/statements/grant-transact-sql) CREATE QUEUE、CREATE SERVICE 和 CREATE SCHEMA 權限給目標資料庫使用者。|  
||如果尚未以目標資料庫使用者連接到資料庫，請立刻執行此動作。|  
||[建立佇列](/sql/t-sql/statements/create-queue-transact-sql) 來接收事件通知訊息，並 [建立服務](/sql/t-sql/statements/create-service-transact-sql) 來傳遞訊息。|  
||在目標服務上[授與 SEND 權限](/sql/t-sql/statements/grant-transact-sql) 給來源資料庫使用者。|  
|提供來源資料庫的 Service Broker 識別碼給目標伺服器。 此識別碼可利用查詢 **sys.databases** 目錄檢視的 [service_broker_guid](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 資料行取得。 若為伺服器層級事件通知，請使用 **msdb**的 Service Broker 識別碼。|提供目標資料庫的 Service Broker 識別碼給來源伺服器。|  
  
 **步驟 4：建立路由及設定伺服器層級驗證。**  
  
 在來源和目標伺服器上完成下列動作。  
  
|來源伺服器|目標伺服器|  
|-------------------|-------------------|  
|[建立路由](/sql/t-sql/statements/create-route-transact-sql) 到目標服務，並指定目標資料庫的 Service Broker 識別碼和已同意的 TCP 通訊埠編號。|建立路由到來源服務，並指定來源資料庫的 Service Broker 識別碼和已同意的 TCP 通訊埠編號。 若要指定來源服務，請使用下列提供的服務： `https://schemas.microsoft.com/SQL/Notifications/EventNotificationService`。|  
|切換到 **master** 資料庫來設定伺服器層級驗證。|切換到 **master** 資料庫來設定伺服器層級驗證。|  
|如果 **master** 資料庫沒有主要金鑰，請 [建立主要金鑰](/sql/t-sql/statements/create-master-key-transact-sql)。|如果 **master** 資料庫沒有主要金鑰，請建立主要金鑰。|  
|[建立憑證](/sql/t-sql/statements/create-certificate-transact-sql) 來驗證資料庫。|建立憑證來驗證資料庫。|  
|[備份憑證](/sql/t-sql/statements/backup-certificate-transact-sql) 到可供目標伺服器存取的檔案。|備份憑證到可供來源伺服器存取的檔案。|  
|[建立端點](/sql/t-sql/statements/create-endpoint-transact-sql)，並指定已同意的 TCP 通訊埠編號、FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE 憑證名稱  ) 和驗證的憑證名稱。|建立端點，並指定已同意的 TCP 通訊埠編號、FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE 憑證名稱  ) 和驗證憑證的名稱。|  
|[建立登入](/sql/t-sql/statements/create-login-transact-sql)，並指定目標伺服器的登入。|建立登入，並指定來源伺服器的登入。|  
|在端點[授與 CONNECT 權限](/sql/t-sql/statements/grant-transact-sql) 給目標驗證器登入。|在端點授與 CONNECT 權限給來源驗證器登入。|  
|[建立使用者](/sql/t-sql/statements/create-user-transact-sql)，並指定目標驗證器登入。|建立使用者，並指定來源驗證器登入。|  
  
 **步驟 5：共用伺服器層級驗證的憑證並建立事件通知。**  
  
 在來源和目標伺服器上完成下列動作。  
  
|來源伺服器|目標伺服器|  
|-------------------|-------------------|  
|從目標憑證的備份檔案[建立憑證](/sql/t-sql/statements/create-certificate-transact-sql) 時，指定目標驗證器使用者作為擁有者。|從來源憑證的備份檔案建立憑證時，指定來源驗證器使用者作為擁有者。|  
|切換到要建立事件通知的來源資料庫，如果您尚未以來源資料庫使用者連接，請立刻執行此動作。|切換到目標資料庫來接收事件通知訊息。|  
|[建立事件通知](/sql/t-sql/statements/create-event-notification-transact-sql)，並指定 Broker Service 和目標資料庫的識別碼。||  
  
## <a name="see-also"></a>另請參閱  
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [加密階層](../security/encryption/encryption-hierarchy.md)   
 [實作事件通知](event-notifications.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-remote-service-binding-transact-sql)   
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-queue-transact-sql)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-service-transact-sql)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-notification-transact-sql)  
  
  
