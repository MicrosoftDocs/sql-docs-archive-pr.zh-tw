---
title: 使用 sql： identity 和 sql： guid 注釋 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
author: rothja
ms.author: jroth
ms.openlocfilehash: dc5c08f158911edb0a1a0638fc4bcee1e05a248c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595906"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>使用 sql:identity 和 sql:guid 註解
  您可以在 `sql:identity` `sql:guid` 對應至中資料庫資料行的任何節點上，于 XSD 架構中指定和批註 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 updategram 格式支援 `updg:at-identity` 和 `updg:guid` 屬性，而 DiffGram 格式則不支援。 `updg:at-identity` 屬性會定義更新 IDENTITY 類型之資料行時的行為。 `updg:guid` 屬性可讓您從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 取得 GUID 值，並將其用在 updategram 中。 如需詳細資訊和工作範例，請參閱[使用 XML Updategram 插入資料 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
 `sql:identity` 和 `sql:guid` 註解會將此功能擴充到 DiffGrams。  
  
 當您執行 DiffGram 時，會先將其轉換為 updategram，然後再執行 updategram。 透過在 XSD 結構描述中指定 `sql:identity` 和 `sql:guid` 註解，您實際上就在定義 updategram 的行為。 因此，所有註解的描述都在 updategram 的內容中。 註解可以同時用於 DiffGrams 和 updategrams，不過，updategrams 已經提供更強大的方式來處理識別與 GUID 值。  
  
 `sql:identity` 和 `sql:guid` 註解可以在複雜內容元素上定義。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 註解  
 您可以在對應到 IDENTITY 類型之資料庫資料行的任何節點上，指定 XSD 結構描述的 `sql:identity` 註解。 針對此批註指定的值會定義如何使用 updategram 中提供的值來修改資料行，或藉由忽略值來 (更新識別類型資料行，在此情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將產生的值用於此資料行) 。  
  
 系統可以指派兩個值給 `sql:identity` 註解：  
  
 ignore  
 導向 updategram 忽略 updategram 中針對該資料行提供的任何值，並依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生識別值。  
  
 useValue  
 導向 updategram 使用 updategram 中提供的值，來更新 IDENTITY 類型的資料行。 updategram 不會檢查資料行是否是識別值。  
  
 如果 updategram 指定 IDENTITY 類型資料行的值，必須在結構描述中指定 `sql:identity="useValue"`。  
  
## <a name="sqlguid-annotation"></a>sql:guid 註解  
 updategram 可以讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生 GUID 值，然後在 updategram 中使用此值。 在 DiffGrams 的內容中，您可以使用 `sql:guid` 註解來指定要使用 SQL Server 所產生的 GUID 值，還是使用 updategram 中針對該資料行提供的值。  
  
 系統可以指派兩個值給 `sql:guid` 註解：  
  
 generate  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所產生的 GUID 用於更新作業中的該資料行。  
  
 useValue  
 指定在 updategram 中指定的值用於該資料行。 這是預設值。  
  
  
