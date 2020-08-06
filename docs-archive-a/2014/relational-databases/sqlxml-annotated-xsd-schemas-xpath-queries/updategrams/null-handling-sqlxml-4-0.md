---
title: Null 處理 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: rothja
ms.author: jroth
ms.openlocfilehash: 430643e8a6c9bd3dd00b2763990645c6a162ee40
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597747"
---
# <a name="null-handling-sqlxml-40"></a>NULL 處理 (SQLXML 4.0)
  XML 語法表示 NULL 不存在   (例如，如果屬性或專案值為 Null，則 XML 檔中不存在該屬性或元素。在 SQLXML 中 ) [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ， `updg:nullvalue` 屬性可為元素或屬性值指定 Null。  
  
 例如，下列 updategram 可確保**ContactID**為64之連絡人的**標題**值為 Null，然後將**標題**值更新為「Mr」。 。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 當參數傳遞到 Updategram 時，NULL 可以當做參數值傳遞。 這可以透過指定 `nullvalue` 區塊中的 `<updg:header>` 屬性完成。 如需範例，請參閱[將參數傳遞至 updategram &#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全性考慮](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
