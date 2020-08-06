---
title: SQLXML 4.0 的指導方針和限制 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
ms.assetid: fe433d30-90a1-421e-85c6-af13294dc18d
author: rothja
ms.author: jroth
ms.openlocfilehash: e020cbf0ac32e4c878b0b74b67e7c9c679d5d178
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584359"
---
# <a name="guidelines-and-limitations-of-sqlxml-40"></a>SQLXML 4.0 的指導方針和限制
  當您使用 SQLXML 4.0 時，請記住以下事項：  
  
-   當做查詢結果傳回的 XML 不會針對產生此 XML 的對應結構描述進行驗證。  
  
-   SQLXML 4.0 同時包含與版本無關以及與版本相關的 PROGID。 建議您所有的實際執行應用程式都應該使用與版本相關的 PROGID。 這一點特別重要，因為 SQLXML 4.0 並非完全具有回溯相容性。 當您安裝更新的版本時，使用與版本相關的 PROGID 會防止您的實際執行可能發生的失敗。 在不同的版本之間，程式行為可能會因為各種原因而失敗，例如錯誤修正、可能的設計變更等等。 當您安裝更新的版本時，使用與版本相關的 PROGID 會防止發生非預期的失敗。 如果在您安裝更新的版本時使用與版本相關的 PROGID，您的應用程式將會繼續運作，而不會發生失敗。 如果您決定變更與之前版本相關的 PROGID，並在較新的版本中使用與最近版本相關的 PROGID，您必須先測試應用程式，然後才能實際執行它。 例如，使用與版本無關之 PROGID 的應用程式可能會在以下案例中發生失敗：  
  
     您正在執行使用 SQLXML 4.0 以及與版本無關之 PROGID 的應用程式，而且您決定安裝某個其他軟體程式。 此程式可能會安裝舊版的 SQLXML。 您的應用程式可能會失敗，因為應用程式內與版本無關的 PROGIDS 現在指向舊版的 SQLXML，它不一定擁有您的應用程式所使用的 SQLXML 功能。  
  
-   如果您因為任何原因而不想使用 SQLXMLOLEDB 提供者，而想要使用 SQLXML 提供者的功能，請將**Sqlxml Version**屬性設定為 "sqlxml. 4.0"。  
  
  
