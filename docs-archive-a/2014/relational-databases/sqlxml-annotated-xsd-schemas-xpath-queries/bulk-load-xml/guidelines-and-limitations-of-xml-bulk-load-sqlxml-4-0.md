---
title: XML 大量載入的指導方針和限制 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
author: rothja
ms.author: jroth
ms.openlocfilehash: 08c0020ac7b28702f5a573c6158ec9d50c735b2a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597754"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 大量載入的指導方針和限制 (SQLXML 4.0)
  當您使用 XML 大量載入時，應該先熟悉下列指導方針和限制：  
  
-   不支援內嵌結構描述。  
  
     如果您的 XML 來源文件中有一個內嵌結構描述，XML 大量載入會忽略該結構描述。 您會針對 XML 資料外部的 XML 大量載入，指定對應的結構描述。 您不能使用**xmlns = "x:schema"** 屬性，在節點上指定對應架構。  
  
-   XML 文件已確認格式正確，但尚未經過驗證。  
  
     XML 大量載入會檢查 XML 檔，以判斷它的格式是否正確，也就是確保 XML 符合全球資訊網協會的 XML 1.0 建議的語法需求。 如果文件的格式不正確，XML 大量載入會取消處理並傳回錯誤。 唯一的例外是當文件為片段 (例如，文件沒有單一的根元素) 時，在此情況下，XML 大量載入將會載入文件。  
  
     XML 大量載入不會針對 XML 資料檔中定義或參考的任何 XML 資料或 DTD 結構描述驗證文件。 此外，XML 大量載入不會根據提供的對應結構描述驗證 XML 資料檔。  
  
-   系統會忽略任何 XML 初構資訊。  
  
     XML 大量載入會忽略 \<root> xml 檔中元素之前和之後的所有資訊。 例如，XML 大量載入會忽略任何 XML 宣告、內部 DTD 定義、外部 DTD 參考、註解等等。  
  
-   如果您擁有的對應結構描述會定義兩個資料表之間 (例如 Customer 和 CustOrder 之間) 的主索引鍵/外部索引鍵關聯性，則必須先在結構描述中描述具有主索引鍵的資料表。 包含外部索引鍵資料行的資料表稍後必須出現在結構描述中。 這是因為在架構中識別資料表的順序，是用來將它們載入資料庫的順序。例如，下列 XDR 架構在 XML 大量載入中使用時會產生錯誤，因為元素會在專案 **\<Order>** 之前描述 **\<Customer>** 。 在 CustOrder 中的 CustomerID 資料行是外部索引鍵資料行，它會參考在 Cust 資料表中的 CustomerID 主索引鍵資料行。  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
        <ElementType name="Order" sql:relation="CustOrder" >  
          <AttributeType name="OrderID" />  
          <AttributeType name="CustomerID" />  
          <attribute type="OrderID" />  
          <attribute type="CustomerID" />  
        </ElementType>  
  
       <ElementType name="CustomerID" dt:type="int" />  
       <ElementType name="CompanyName" dt:type="string" />  
       <ElementType name="City" dt:type="string" />  
  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
       <ElementType name="Customers" sql:relation="Cust"   
                         sql:overflow-field="OverflowColumn"  >  
          <element type="CustomerID" sql:field="CustomerID" />  
          <element type="CompanyName" sql:field="CompanyName" />  
          <element type="City" sql:field="City" />  
          <element type="Order" >   
               <sql:relationship  
                   key-relation="Cust"  
                    key="CustomerID"  
                    foreign-key="CustomerID"  
                    foreign-relation="CustOrder" />  
          </element>  
       </ElementType>  
    </Schema>  
    ```  
  
-   如果結構描述沒有使用 `sql:overflow-field` 註解指定溢位資料行，XML 大量載入會忽略顯示在 XML 文件中的任何資料，但是不會在對應結構描述中描述。  
  
     每當 XML 大量載入在 XML 資料流中碰到已知的標記時，會套用您所指定的對應結構描述。 它會忽略顯示在 XML 文件中的資料，但是不會在結構描述中描述。 例如，假設您有一個描述元素的對應架構 **\<Customer>** 。 XML 資料檔案具有根標籤 **\<AllCustomers>** (，不會在括住所有元素的架構) 中加以描述 **\<Customer>** ：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     在此情況下，XML 大量載入會忽略 **\<AllCustomers>** 元素，並在專案開始對應 **\<Customer>** 。 XML 大量載入會忽略結構描述中沒有描述但是顯示在 XML 文件中的元素。  
  
     請考慮包含元素的另一個 XML 源資料檔案 **\<Order>** 。 這些元素不會在對應的結構描述中描述：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      ...  
    </AllCustomers>  
    ```  
  
     XML 大量載入會忽略這些 **\<Order>** 元素。 但是，如果您在 `sql:overflow-field` 架構中使用批註來識別資料行做為溢位資料行，則 XML 大量載入會將所有未耗用的資料儲存在此資料行中。  
  
-   CDATA 區段和實體參考會在儲存在資料庫之前，先轉譯成其對等字串。  
  
     在此範例中，CDATA 區段會包裝元素的值 **\<City>** 。 XML 大量載入會先將字串值 ( "NY" ) ，再將 **\<City>** 元素插入資料庫中。  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 大量載入不會保留實體參考。  
  
-   如果對應結構描述指定屬性的預設值，而且 XML 來源資料不包含該屬性，XML 大量載入會使用預設值。  
  
     下列範例 XDR 架構會將預設值指派給**雇用**項屬性：  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
  
       <ElementType name="Customers" sql:relation="Cust3" >  
          <AttributeType name="CustomerID" dt:type="int"  />  
          <AttributeType name="HireDate"  default="2000-01-01" />  
          <AttributeType name="Salary"   />  
  
          <attribute type="CustomerID" sql:field="CustomerID" />  
          <attribute type="HireDate"   sql:field="HireDate"  />  
          <attribute type="Salary"     sql:field="Salary"    />  
       </ElementType>  
    </Schema>  
    ```  
  
     在此 XML 資料中，第二個元素中遺漏了「**雇用**項」屬性 **\<Customers>** 。 當 XML 大量載入將第二個 **\<Customers>** 元素插入資料庫時，它會使用架構中指定的預設值。  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   不支援 `sql:url-encode` 註解：  
  
     您無法在 XML 資料輸入中指定 URL，然後預期大量載入會從該位置讀取資料。  
  
     系統會建立在對應結構描述中所識別的資料表 (資料庫必須存在)。 如果資料庫中已經有一或多個資料表存在，SGDropTables 屬性會決定是否要卸載並重新建立這些預先存在的資料表。  
  
-   如果您指定 SchemaGen 屬性 (例如，SchemaGen = true) ，則會建立對應架構中所識別的資料表。 但是，SchemaGen 不會建立任何條件約束 (例如，) 這些資料表的 PRIMARY KEY/FOREIGN KEY 條件約束，但有一個例外：如果在關聯性中組成主鍵的 XML 節點定義為具有識別碼的 XML 類型 (也就是 `type="xsd:ID"` 針對 XSD) 而且 SGUseID 屬性設定為 True （針對 SchemaGen），則不只是從識別碼類型節點建立的主鍵，而是從對應架構關聯性建立主鍵/外鍵關聯性。  
  
-   SchemaGen 不會使用 XSD 架構 facet 和延伸模組來產生關聯式 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 架構。  
  
-   如果您指定 SchemaGen 屬性 (例如，SchemaGen = true) 在大量載入上，則只會更新指定之共用名稱) 的資料表 (而不會更新。  
  
-   SchemaGen 只提供從批註式 XSD 產生關聯式架構的基本功能。 如果需要，使用者應該手動修改產生的資料表。  
  
-   當資料表之間存在多個關聯性時，SchemaGen 會嘗試建立單一關聯性，其中包含兩個數據表之間的所有相關索引鍵。 這個限制可能是 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 錯誤的原因。  
  
-   當您將 XML 資料大量載入資料庫時，在對應結構描述中至少要有一個對應到資料庫資料行的屬性或子元素。  
  
-   如果您要使用 XML 大量載入來插入日期值，必須以 (-)CCYY-MM-DD((+-)TZ) 格式指定這些值。 這是用於日期的標準 XSD 格式。  
  
-   某些屬性旗標與其他屬性旗標不相容。 例如，大量載入不同時支援 `Ignoreduplicatekeys=true` 及 `Keepidentity=false`。 `Keepidentity=false` 時，大量載入需要伺服器才能產生索引鍵值。 資料表在索引鍵上應該要有 `IDENTITY` 條件約束。 伺服器不會產生重複的索引鍵，這表示不需要將 `Ignoreduplicatekeys` 設定為 `true`。 只有在下列兩種情況下才需要將 `Ignoreduplicatekeys` 設定為 `true`：從內送資料上傳主索引鍵值到具有資料列的資料表以及可能會發生主索引鍵值衝突時。  
  
  
