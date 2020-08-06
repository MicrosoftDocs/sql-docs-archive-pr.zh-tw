---
title: 屬性關聯性 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- member properties [Analysis Services], attribute relationships
- security [Analysis Services], properties
- PROPERTIES keyword
- storage [Analysis Services], attribute relationships
- natural hierarchies [Analysis Services]
- dimensions [Analysis Services], member properties
- queries [MDX], attribute relationships
- user-defined hierarchies [Analysis Services]
- attributes [Analysis Services], relationships
- member properties [Analysis Services]
- members [Analysis Services], attribute relationships
- storing data [Analysis Services], attribute relationships
- relationships [Analysis Services], attributes
ms.assetid: 2491422a-4cf5-4b23-b6ab-289222b22ce8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 122638a2728a8a85ee58661196797383da20eef8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702028"
---
# <a name="attribute-relationships"></a>屬性關聯性
  在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，維度內的屬性永遠都是直接或間接與索引鍵屬性相關。 當您根據所有維度屬性都是衍生自相同關聯式資料表的星狀結構描述來定義維度時，便會在索引鍵屬性和維度的每個非索引鍵屬性之間，自動定義屬性關聯性。 而根據維度屬性是衍生自多個相關資料表的雪花式結構描述來定義維度時，便會自動定義下列的屬性關聯性：  
  
-   索引鍵屬性和繫結到主維度資料表之資料行的每個非索引鍵屬性之間。  
  
-   索引鍵屬性和繫結到連結基礎維度資料表之次要資料表的外部索引鍵屬性之間。  
  
-   在繫結到次要資料表之外部索引鍵的屬性和繫結到次要資料表中之資料行的非索引鍵屬性之間。  
  
 然而，您可能會需要變更這些預設的屬性關聯性。 例如，您可能會想要定義自然階層、自訂排序順序或依據非索引鍵屬性的維度資料粒度。 如需詳細資訊，請參閱[維度屬性屬性參考](../multidimensional-models/dimension-attribute-properties-reference.md)。  
  
> [!NOTE]  
>  在多維度運算式 (MDX) 中，屬性關聯性就是所謂的成員屬性。  
  
## <a name="natural-hierarchy-relationships"></a>自然階層關聯性  
 當使用者自訂階層中所含的每一個屬性有一對多的關聯性，而且底下緊接著該屬性時，此階層就是自然階層。 例如，假設客戶維度所依據的關聯式來源資料表中有八個資料行：  
  
-   CustomerKey  
  
-   CustomerName  
  
-   年齡  
  
-   性別  
  
-   電子郵件  
  
-   城市  
  
-   Country  
  
-   區域  
  
 對應的 Analysis Services 維度有七個屬性：  
  
-   客戶 (根據 CustomerKey，使用 CustomerName 提供成員名稱)  
  
-   年齡、性別、電子郵件、城市、區域、國家 (地區)  
  
 代表自然階層之關聯性的強制執行方式，是在某層級的屬性以及該層級底下之層級的屬性之間建立屬性關聯性。 若是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，這樣會指定自然關聯性與潛在彙總。 在客戶維度中，國家 (地區)、區域、城市和客戶等屬性都存在著自然階層。 `{Country, Region, City, Customer}` 的自然階層，會藉由加入下列屬性關聯性來描述：  
  
-   國家 (地區) 屬性與區域屬性之間的屬性關聯性。  
  
-   區域屬性與城市屬性之間的屬性關聯性。  
  
-   城市屬性與客戶屬性之間的屬性關聯性。  
  
 若要導覽 cube 中的資料，您也可以建立使用者定義階層，此階層不代表資料 (中的自然階層，稱為臨機操作*或**報表*階層) 。 例如，您可以根據 `{Age, Gender}` 建立使用者自訂階層。 使用者不會看到這兩個階層的行為有何差異，雖然自然階層會受益于匯總和編制索引結構，也就是在來源資料中的自然關聯性的帳戶。  
  
 層級的 `SourceAttribute` 屬性 (Property) 會決定該使用哪個屬性 (Attribute) 來描述層級。 屬性 (Attribute) 上的 `KeyColumns` 屬性 (Property) 會指定資料來源檢視中，提供成員的資料行。 屬性 (Attribute) 上的 `NameColumn` 屬性 (Property) 可為成員指定不同的名稱資料行。  
  
 若要使用定義使用者自訂階層中的層級 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，**維度設計師**可讓您選取維度屬性、維度資料表中的資料行，或從 cube 的資料來源視圖中所包含的相關資料表中選取資料行。 如需建立使用者定義階層的詳細資訊，請參閱[建立使用者定義](../multidimensional-models/user-defined-hierarchies-create.md)階層。  
  
 在 Analysis Services 中，通常會對成員的內容進行假設。 分葉成員並沒有下階，且包含衍生自基礎資料來源的資料。 非分葉成員具有下階，且包含衍生自在子成員上執行之彙總的資料。 在彙總層級中，成員是以從屬層級的彙總為基礎。 因此，若在層級的來源屬性 (Attribute) 上，將 `IsAggregatable` 屬性 (Property) 設定為 `False` 時，就不應加入可彙總的屬性 (Attribute) 作為其上層級。  
  
## <a name="defining-an-attribute-relationship"></a>定義屬性關聯性  
 當您建立屬性關聯性時，其主要條件約束是要確定屬性關聯性所參考的屬性，在屬性關聯性所屬的屬性中，任何成員只有一個值。 例如，如果您在城市屬性與省份屬性間定義關聯性，每個城市就只能和單一省份相關。  
  
## <a name="attribute-relationship-queries"></a>屬性關聯性查詢  
 您可以使用 MDX 查詢，利用 MDX `PROPERTIES` 陳述式的 `SELECT` 關鍵字，從屬性關聯性中擷取成員屬性形式的資料。 如需如何使用 MDX 來取得成員屬性的詳細資訊，請參閱[使用成員屬性 &#40;MDX&#41;](../multidimensional-models/mdx/mdx-member-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](attributes-and-attribute-hierarchies.md)   
 [維度屬性屬性參考](../multidimensional-models/dimension-attribute-properties-reference.md)   
 [使用者階層](user-hierarchies.md)   
 [使用者階層屬性](user-hierarchies-properties.md)  
  
  
