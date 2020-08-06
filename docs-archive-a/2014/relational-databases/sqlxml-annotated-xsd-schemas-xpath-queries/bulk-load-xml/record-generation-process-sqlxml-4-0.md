---
title: 記錄產生進程 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], record generation process
- node scopes [SQLXML]
- record subsets [SQLXML]
- scope [SQLXML]
- key ordering rules [SQLXML]
- record generation process for bulk loads [SQLXML]
- entering node scope [SQLXML]
- bulk load [SQLXML], record generation process
- leaving node scope [SQLXML]
- schema mapping [SQLXML]
ms.assetid: d8885bbe-6f15-4fb9-9684-ca7883cfe9ac
author: rothja
ms.author: jroth
ms.openlocfilehash: 5734776864aecbda7adaf0b9b16180b5ebd55ce3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686875"
---
# <a name="record-generation-process-sqlxml-40"></a>記錄產生處理序 (SQLXML 4.0)
  XML 大量載入會處理 XML 輸入資料，並在 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中為適當的資料表準備記錄。 XML 大量載入的邏輯會判斷在何時產生新記錄，要複製哪種子元素或屬性值到記錄欄位中，以及記錄何時會完成並準備傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以供插入之用。  
  
 XML 大量載入不會將整個 XML 輸入資料載入到記憶體中，也不會在將資料傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前產生完整的記錄集。 這是因為 XML 輸入資料可以是大型文件，而且將整個文件載入到記憶體中的成本可能會很高。 XML 大量載入會改為執行下列動作：  
  
1.  分析對應結構描述和準備需要的執行計畫。  
  
2.  將執行計畫套用到輸入資料流中的資料。  
  
 這個循序處理對於以特殊方式提供 XML 輸入資料而言很重要。 您必須了解 XML 大量載入是如何分析對應結構描述，以及了解記錄產生處理序是如何發生的。 有了這樣的了解，您就可以為 XML 大量載入提供會產生您想要結果的對應結構描述。  
  
 XML 大量載入會處理一般對應結構描述註解，包括資料行和資料表對應 (藉由使用註解明確指定，或透過預設對應隱含指定)，並聯結關聯性。  
  
> [!NOTE]  
>  假設您熟悉註解式 XSD 或 XDR 對應結構描述。 如需有關架構的詳細資訊，請參閱[批註式 XSD 架構簡介 &#40;sqlxml 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)或[&#40;已在 sqlxml 4.0&#41;中取代的批註式 XDR 架構](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
 了解記錄產生之前，需要先了解下列概念：  
  
-   節點範圍  
  
-   記錄產生規則  
  
-   記錄子集和索引鍵排列順序規則  
  
-   記錄產生規則的例外狀況  
  
## <a name="scope-of-a-node"></a>節點範圍  
 當 XML 大量載入在 XML 輸入資料流程中遇到時，節點 (XML 檔中的元素或屬性) 進入*範圍*。 如果是元素節點，元素的開始標記會將元素納入範圍中。 如果是屬性節點，屬性名稱會將屬性納入範圍中。  
  
 當節點沒有更多資料時，就會離開範圍：可能是在結束標記 (在元素節點的狀況下)，或是在屬性值的結尾 (在屬性節點的狀況下)。  
  
## <a name="record-generation-rule"></a>記錄產生規則  
 當節點 (元素或屬性) 進入範圍內時，記錄可能會從該節點產生。 只要相關聯的節點在範圍內，記錄就會一直存在。 當節點離開範圍時，XML 大量載入會視為產生的記錄是完整的 (具有資料)，並將它傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 供插入之用。  
  
 例如，請考慮下列 XSD 結構描述片段：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Customers" >  
   <xsd:complexType>  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
     <xsd:attribute name="CompanyName" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 架構會指定 **\<Customer>** 具有**CustomerID**和**公司名稱**屬性的元素。 批註會將 `sql:relation` **\<Customer>** 元素對應至 Customers 資料表。  
  
 請考慮這個 XML 文件的片段：  
  
```  
<Customer CustomerID="1" CompanyName="xyz" />  
<Customer CustomerID="2" CompanyName="abc" />  
...  
```  
  
 當 XML 大量載入是由結構描述提供，而該結構描述在前面段落和 XML 資料中是描述為輸入時，則 XML 大量載入會在來源資料中處理節點 (元素和屬性)，如下所示：  
  
-   第一個元素的開始標記 **\<Customer>** 會將該元素帶入範圍中。 這個節點會對應到「客戶」資料表。 因此，XML 大量載入會產生「客戶」資料表的記錄。  
  
-   在架構中，元素的所有屬性都會 **\<Customer>** 對應到 Customers 資料表的資料行。 當這些屬性進入範圍內時，XML 大量載入會將屬性值複製到已由父範圍產生的客戶記錄中。  
  
-   當 XML 大量載入到達元素的結束標記時 **\<Customer>** ，元素會超出範圍。 這會造成 XML 大量載入將記錄視為已完成並將之傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 XML 大量載入會針對每個後續元素，遵循此程式 **\<Customer>** 。  
  
> [!IMPORTANT]  
>  在這個模型中，因為在到達結束標記時 (或節點離開範圍時) 會插入記錄，所以您必須定義與在節點範圍內之記錄相關聯的所有資料。  
  
## <a name="record-subset-and-the-key-ordering-rule"></a>記錄子集和索引鍵排列順序規則  
 當您指定使用 `<sql:relationship>` 的對應結構描述時，子集詞彙會參考在關聯性外部端上產生的記錄。 在下列範例中，CustOrder 記錄是在外部端 `<sql:relationship>`。  
  
 例如，假設資料庫包含下列資料表：  
  
-   Cust (CustomerID、CompanyName、City)  
  
-   CustOrder (CustomerID、OrderID)  
  
 在 CustOrder 資料表中的 CustomerID 是外部索引鍵，會參考在 Cust 資料表中的 CustomerID 主要索引鍵。  
  
 現在，請將 XML 檢視視為是在下列註解式 XSD 結構描述中所指定。 這個結構描述使用 `<sql:relationship>` 指定 Cust 和 CustOrder 資料表之間的關聯性。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 範例 XML 資料和建立工作範例的步驟如下。  
  
-   當 **\<Customer>** xml 資料檔案中的元素節點進入範圍內時，Xml 大量載入會產生「加入」資料表的記錄。 然後，XML 大量載入會從、和子專案中，將必要的資料行值複製 (CustomerID、公司名稱和 City) **\<CustomerID>** ，因為這些專案會在 **\<CompanyName>** 範圍中 **\<City>** 輸入這些元素。  
  
-   當 **\<Order>** 元素節點進入範圍內時，XML 大量載入會產生 CustOrder 資料表的記錄。 XML 大量載入會將 [**訂單**] 屬性的值複製到此記錄。 CustomerID 資料行所需的值是從元素的 **\<CustomerID>** 子項目取得 **\<Customer>** 。 除非在元素中指定 Customerid 屬性，否則 XML 大量載入會使用中指定的資訊 `<sql:relationship>` 來取得此記錄的**CustomerID** customerid 外鍵值 **\<Order>** 。 一般規則是，如果子元素明確指定外部索引鍵屬性的值，則 XML 大量載入會使用該值，而且不會藉由使用指定的 `<sql:relationship>` 從父元素取得值。 當此 **\<Order>** 元素節點超出範圍時，XML 大量載入會將記錄傳送至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，然後 **\<Order>** 以相同的方式處理所有後續的元素節點。  
  
-   最後， **\<Customer>** 元素節點超出範圍。 這時候，XML 大量載入會傳送客戶記錄到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 對於 XML 資料流中的所有後續客戶，XML 大量載入都會遵循這個處理序。  
  
 以下是有關對應結構描述的兩個觀察：  
  
-   當架構符合「內含專案」規則 (例如，與客戶相關聯的所有資料和訂單會定義在相關聯的和元素節點的範圍內 **\<Customer>** **\<Order>**) ，大量載入就會成功。  
  
-   在描述 **\<Customer>** 元素時，其子專案是以適當的順序指定。 在此情況下， **\<CustomerID>** 子項目會在子專案之前指定 **\<Order>** 。 這表示在輸入 XML 資料檔案中， **\<CustomerID>** 當 **\<Order>** 元素進入範圍內時，元素值會當做外鍵值使用。 根據「關鍵識別碼順序規則」，要先指定索引鍵屬性。  
  
     如果您指定 **\<CustomerID>** 子專案之後的子項目 **\<Order>** ，當 **\<Order>** 元素進入範圍內時，就無法使用此值。 當結束標記之後，就會將 **\</Order>** CustOrder 資料表的記錄視為 complete，並插入 CustOrder 資料表中，其中包含 CustomerID 資料行的 Null 值，這不是所需的結果。  
  
#### <a name="to-create-a-working-sample"></a>建立工作範例  
  
1.  將這個範例所提供的結構描述儲存為 SampleSchema.xml。  
  
2.  建立這些資料表：  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                 OrderID        int         PRIMARY KEY,  
                 CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
3.  儲存下列範例 XML 輸入資料為 SampleXMLData.xml：  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>   
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
        <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  若要執行 XML 大量載入，請儲存和執行下列 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) 範例 (BulkLoad.vbs)：  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
## <a name="exceptions-to-the-record-generation-rule"></a>記錄產生規則的例外狀況  
 當 XML 大量載入進入範圍內時，不會產生節點記錄 (如果該節點是 IDREF 或 IDREFS 類型的話)。 您必須確定完整的記錄描述會出現在結構描述中的某個地方。 `dt:type="nmtokens"` 註解會被忽略，就像 IDREFS 類型也被忽略一樣。  
  
 例如，請考慮下列描述和元素的 XSD **\<Customer>** 架構 **\<Order>** 。 **\<Customer>** 元素包含 IDREFS 類型的**OrderList**屬性。 `<sql:relationship>` 標記會在客戶和訂單清單之間指定一對多關聯性。  
  
 這是結構描述：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
                 parent="Cust"  
                 parent-key="CustomerID"  
                 child="CustOrder"  
                 child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="CompanyName" type="xsd:string" />  
    <xsd:attribute name="City" type="xsd:string" />  
    <xsd:attribute name="OrderList"   
                       type="xsd:IDREFS"   
                       sql:relation="CustOrder"   
                       sql:field="OrderID"  
                       sql:relationship="CustCustOrder" >  
    </xsd:attribute>  
  </xsd:complexType>  
 </xsd:element>  
  
  <xsd:element name="Order" sql:relation="CustOrder" >  
   <xsd:complexType>  
    <xsd:attribute name="OrderID" type="xsd:string" />  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="OrderDate" type="xsd:date" />  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 由於大量載入會忽略 IDREFS 類型的節點，因此當 [ **OrderList**屬性] 節點進入範圍內時，不會產生任何記錄。 因此，如果您希望訂單記錄加入「訂單」資料表中，您必須描述那些在結構描述某處的訂單。 在此架構中，指定 **\<Order>** 元素可確保 XML 大量載入會將訂單記錄新增至 Orders 資料表。 **\<Order>** 元素會描述填滿 CustOrder 資料表記錄所需的所有屬性。  
  
 您必須確定元素中的**CustomerID**和「**訂單**」值 **\<Customer>** 符合專案中的值 **\<Order>** 。 您必須負責維護參考完整性。  
  
#### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  建立這些資料表：  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
                  CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
                  CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID),  
                  OrderDate      datetime DEFAULT '2000-01-01')  
    GO  
    ```  
  
2.  將這個範例所提供的對應結構描述儲存為 SampleSchema.xml。  
  
3.  將下列 XML 資料範例儲存為 SampleXMLData.xml：  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1111" CompanyName="Sean Chai" City="NY"  
                 OrderList="Ord1 Ord2" />  
      <Customers CustomerID="1112" CompanyName="Dont Know" City="LA"  
                 OrderList="Ord3 Ord4" />  
      <Order OrderID="Ord1" CustomerID="1111" OrderDate="1999-01-01" />  
      <Order OrderID="Ord2" CustomerID="1111" OrderDate="1999-02-01" />  
      <Order OrderID="Ord3" CustomerID="1112" OrderDate="1999-03-01" />  
      <Order OrderID="Ord4" CustomerID="1112" OrderDate="1999-04-01" />  
    </ROOT>  
    ```  
  
4.  若要執行 XML 大量載入，請儲存和執行這個 VBScript 範例 (SampleVB.vbs)：  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
