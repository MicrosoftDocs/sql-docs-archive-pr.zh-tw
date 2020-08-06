---
title: XML 報表資料的元素路徑語法 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ElementPath syntax
- XML [Reporting Services], data retrieval
ms.assetid: 07bd7a4e-fd7a-4a72-9344-3258f7c286d1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b7d66b39761dc278abff25a3b22ccd18ca74272b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710241"
---
# <a name="element-path-syntax-for-xml-report-data-ssrs"></a>XML 報表資料的元素路徑語法 (SSRS)
  在「報表設計師」中，可藉由定義區分大小寫的元素路徑來指定要用於 XML 資料來源中之報表的資料。 元素路徑會指出在 XML 資料來源中周遊 XML 階層式節點及其屬性的方法。 若要使用預設的元素路徑，請將資料集查詢或 XML `ElementPath` (屬於 XML `Query`) 保留空白。 由 XML 資料來源擷取資料時，具有文字值的元素節點以及元素節點屬性會變成結果集內的資料行。 執行查詢時，節點及屬性的值會變成資料列資料。 這些資料行會以資料集欄位集合的方式顯示在 [報表資料] 窗格中。 此主題描述元素路徑語法。  
  
> [!NOTE]  
>  元素路徑與命名空間無關。 若要在專案路徑中使用命名空間，請使用 XML 查詢語法，其中包含 xml `ElementPath` [報表資料 &#40;SSRS&#41;的 Xml 查詢語法](report-data-ssrs.md)中所述的 xml 元素。  
  
 下表描述定義元素路徑所使用的慣例。  
  
|慣例|用於|  
|----------------|--------------|  
|**粗體字**|文字必須完全依照顯示的樣子輸入。|  
|&#124; (分隔號)|會分隔語法項目， 您只能選擇其中一個項目。|  
|`[ ] (brackets)`|選擇性的語法項目。 不要輸入方括號。|  
|**{}** (大括弧) |會分隔語法項目的參數。|  
|[ **,** ...*n*]|指出先前項目可以重複 *n* 次。 以逗號分隔項目。|  
  
## <a name="syntax"></a>語法  
  
```  
  
Element path ::=  
    ElementNode[/Element path]  
ElementNode ::=  
    XMLName[(Encoding)][{[FieldList]}]  
XMLName ::=  
    [NamespacePrefix:]XMLLocalName  
Encoding ::=  
        HTMLEncoded | Base64Encoded  
FieldList ::=  
    Field[,FieldList]  
Field ::=  
    Attribute | Value | Element | ElementNode  
Attribute ::=  
        @XMLName[(Type)]  
Value ::=  
        @[(Type)]  
Element ::=  
    XMLName[(Type)]  
Type ::=  
        String | Integer | Boolean | Float | Decimal | Date | XML   
NamespacePrefix ::=  
    Identifier that specifies the namespace.  
XMLLocalName :: =  
    Identifier in the XML tag.   
```  
  
## <a name="remarks"></a>備註  
 下表摘要說明元素路徑的詞彙。 表格中的範例會參考範例 XML 文件 Customers.xml (包含在本主題的「範例」一節中)。  
  
> [!NOTE]  
>  XML 標記有區分大小寫。 在元素路徑中指定 ElementNode 時，必須完全符合資料來源中的 XML 標記。  
  
|詞彙|定義|  
|----------|----------------|  
|元素路徑|定義 XML 文件中周遊節點的順序，以便使用 XML 資料來源擷取資料集的欄位資料。|  
|`ElementNode`|XML 文件中的 XML 節點。 節點是由標記指定，並存在於與其他節點構成的階層式關聯性中。 例如， \<Customers> 是根項目節點。 \<Customer>是的子項目 \<Customers> 。|  
|`XMLName`|節點的名稱。 例如，Customers 節點的名稱為 Customers。 `XMLName` 可以使用命名空間識別碼做為前置詞，以確保所有節點的名稱都是唯一的。|  
|`Encoding`|指出本元素的 `Value` 是已編碼的 XML，需要加以解碼並加入做為此元素的子元素。|  
|`FieldList`|定義用來擷取資料的元素與屬性組合。<br /><br /> 如果沒有指定，所有屬性和子元素都會做為欄位使用。 如果指定了空的欄位清單 (**{}**) ，就不會使用這個節點中的任何欄位。<br /><br /> `FieldList` 可能不會同時包含 `Value` 及 `Element` 或 `ElementNode`。|  
|`Field`|指定擷取做為資料集欄位的資料。|  
|`Attribute`|`ElementNode` 中名稱與值的配對。 例如，在專案節點中 \<Customer ID="1"> ， `ID` 是屬性，並會 `@ID(Integer)` 在對應的資料欄位中傳回 "1" 做為整數類型 `ID` 。|  
|`Value`|項目的值。 `Value` 只能用於元素路徑中的最後一個 `ElementNode` 上。 例如，因為 \<Return> 是分葉節點，如果您將它包含在元素路徑的結尾，則的值 `Return {@}` 會是 `Chair` 。|  
|`Element`|具名子元素的值。 例如，Customers {}/Customer {}/LastName 只會擷取 LastName 元素的值。|  
|`Type`|此元素建立之欄位所使用的選擇性資料類型。|  
|`NamespacePrefix`|`NamespacePrefix` 是在 XML 查詢元素中定義。 如果 XML 查詢元素不存在，則會省略 XML `ElementPath` 中的命名空間。 如果有 XML 查詢元素，XML `ElementPath` 則會有選擇性的 `IgnoreNamespaces` 屬性。 如果 IgnoreNamespaces 為 `true` ，則 xml 和 xml 檔中的命名空間 `ElementPath` 會被忽略。 如需詳細資訊，請參閱 [XML 報表資料的 XML 查詢語法 &#40;SSRS&#41;](report-data-ssrs.md)。|  
  
## <a name="example---no-namespaces"></a>範例 - 沒有命名空間  
 下列範例會使用 XML 文件 Customers.xml。 這個表格會顯示元素路徑語法的範例，並且以 XML 文件為資料來源，顯示在定義資料集的查詢中使用元素路徑的結果。  
  
 請注意，當元素路徑是空的時，查詢會使用預設的元素路徑：第一個分葉節點集合的路徑。 在第一個範例中，將元素路徑保留為空白相當於將元素路徑指定為 /Customers/Customer/Orders/Order。 路徑上的所有節點值和屬性都會傳回到結果集，而節點名稱和屬性會以資料集欄位的方式顯示。  
  
-   *空白*  
  
    |單|數量|識別碼|名字|姓氏|Customer.ID|xmlns|  
    |-----------|---------|--------|---------------|--------------|-----------------|-----------|  
    |Chair|6|1|Bobby|Moore|11|http://www.adventure-works.com|  
    |資料表|1|2|Bobby|Moore|11|http://www.adventure-works.com|  
    |Sofa|2|8|Crystal|Hu|20|http://www.adventure-works.com|  
    |EndTables|2|15|Wyatt|Diaz|33|http://www.adventure-works.com|  
  
-   `Customers {}/Customer`  
  
    |名字|姓氏|識別碼|  
    |---------------|--------------|--------|  
    |Bobby|Moore|11|  
    |Crystal|Hu|20|  
    |Wyatt|Diaz|33|  
  
-   `Customers {}/Customer {}/LastName`  
  
    |姓氏|  
    |--------------|  
    |Moore|  
    |Hu|  
    |Diaz|  
  
-   `Customers {}/Customer {}/Orders/Order {@,@Qty}`  
  
    |單|數量|  
    |-----------|---------|  
    |Chair|6|  
    |資料表|1|  
    |Sofa|2|  
    |EndTables|2|  
  
-   `Customers {}/Customer/Orders/Order{ @ID(Integer)}`  
  
    |Order.ID|名字|姓氏|識別碼|  
    |--------------|---------------|--------------|--------|  
    |1|Bobby|Moore|11|  
    |2|Bobby|Moore|11|  
    |8|Crystal|Hu|20|  
    |15|Wyatt|Diaz|33|  
  
#### <a name="xml-document-customersxml"></a>XML 文件：Customers.xml  
 若要嘗試前一節中的元素路徑範例，可以複製這段 XML 並將它儲存為報表設計師可以存取的 URL，然後使用 XML 文件做為 XML 資料來源：例如 `http://localhost/Customers.xml`。  
  
```  
<?xml version="1.0"?>  
<Customers xmlns="http://www.adventure-works.com">  
   <Customer ID="11">  
      <FirstName>Bobby</FirstName>  
      <LastName>Moore</LastName>  
      <Orders>  
         <Order ID="1" Qty="6">Chair</Order>  
         <Order ID="2" Qty="1">Table</Order>  
      </Orders>  
      <Returns>  
         <Return ID="1" Qty="2">Chair</Return>  
      </Returns>  
   </Customer>  
   <Customer ID="20">  
      <FirstName>Crystal</FirstName>  
      <LastName>Hu</LastName>  
      <Orders>  
         <Order ID="8" Qty="2">Sofa</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
   <Customer ID="33">  
      <FirstName>Wyatt</FirstName>  
      <LastName>Diaz</LastName>  
      <Orders>  
         <Order ID="15" Qty="2">EndTables</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
</Customers>  
```  
  
 您也可以使用下列程序來建立 XML 資料來源，其中不包含連接字串，查詢中也不內嵌 Customers.XML。  
  
###### <a name="to-embed-customersxml-in-a-query"></a>在查詢中內嵌 Customers.XML  
  
1.  使用空白連接字串建立 XML 資料來源。  
  
2.  建立 XML 資料來源的新資料集。  
  
3.  在 **[資料集屬性]** 對話方塊中，按一下 **[查詢設計工具]**。 以文字為基礎的查詢設計工具對話方塊隨即開啟。  
  
4.  在查詢窗格中，輸入下列兩行程式碼：  
  
     `<Query>`  
  
     `<XmlData>`  
  
5.  複製 Customers.XML，然後將這些文字貼在查詢窗格中的 `<XmlData>`之後。  
  
6.  在查詢窗格中，刪除從 Customers.XML 複製的第一行程式碼： `<?xml version="1.0"?>`  
  
7.  在查詢尾端，加入下列兩行程式碼：  
  
     `<XmlData>`  
  
     `<Query>`  
  
8.  按一下 [執行查詢]**** \(!)。  
  
     結果集會顯示具有下列資料行的 4 行資料： `xmlns`、 `Customer.ID`、 `FirstName`、 `LastName`、 `ID`、 `Qty`、 `Order`。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [XML 連線類型 &#40;SSRS&#41;](xml-connection-type-ssrs.md)   
 [Reporting Services SSRS &#40;的教學課程&#41;](../reporting-services-tutorials-ssrs.md)   
 [加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  
