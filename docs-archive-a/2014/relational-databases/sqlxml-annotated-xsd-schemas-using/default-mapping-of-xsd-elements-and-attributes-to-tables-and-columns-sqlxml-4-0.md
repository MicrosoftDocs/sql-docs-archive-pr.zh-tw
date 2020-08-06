---
title: XSD 元素和屬性對資料表和資料行的預設對應 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XSD schemas [SQLXML], mapping attributes and elements
- mapping schema [SQLXML], default mapping
- element mapping [SQLXML], default mapping
- element mapping [SQLXML]
- table mapping [SQLXML]
- annotated XSD schemas, mapping attributes and elements
- table/view mapping [SQLXML]
- column mapping [SQLXML]
- attribute mapping [SQLXML], default mapping
- default schema mapping
- table mapping [SQLXML], default mapping
- testing XPath query against schema
- xml data type [SQL Server], SQLXML
- table/view mapping [SQLXML], default mapping
- element/attribute mapping [SQLXML]
ms.assetid: 9a18e92a-6cfb-4a14-993a-663a95aabb63
author: rothja
ms.author: jroth
ms.openlocfilehash: 0bccec2413e8a0a6e13283a0f3e5f63ab61e934b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595902"
---
# <a name="default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-40"></a>XSD 元素和屬性對資料表和資料行的預設對應 (SQLXML 4.0)
  根據預設，XSD 註解式結構描述中的複雜類型元素會對應到指定之資料庫中具有相同名稱的資料表 (檢視表)，而簡單類型的元素或屬性會對應到資料表中具有相同名稱的資料行。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱[執行 SQLXML 範例的需求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-default-mapping"></a>A. 指定預設對應  
 在這個範例的 XDR 結構描述中不會指定任何註解。 **\<Person.Contact>** 元素屬於複雜類型，因此預設會對應到 AdventureWorks 資料庫中的 Person 資料表。 元素的所有屬性 (ContactID、FirstName、LastName) **\<Person.Contact>** 都是簡單的類型，而且預設會對應至 Person 資料表中具有相同名稱的資料行。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID"  type="xsd:string" />   
       <xsd:attribute name="FirstName"   type="xsd:string" />   
       <xsd:attribute name="LastName"    type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 MySchema.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 MySchemaT.xml，並放在與儲存 MySchema.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="MySchema.xml">  
            /Person.Contact  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (MySchema.xml) 指定的目錄路徑，相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 部分結果集如下：  
  
```  
<?xml version="1.0" encoding="UTF-8" ?>  
<ROOT>  
  <Person.Contact ContactID="1" FirstName="Gustavo" LastName="Achong"/>  
  <Person.Contact ContactID="2" FirstName="Catherine" LastName="Abel"/>  
   ...  
</ROOT>  
```  
  
### <a name="b-mapping-an-xml-element-to-a-database-column"></a>B. 將 XML 元素對應至資料庫資料行  
 在此範例中，因為沒有使用註解，因此也會發生預設對應。 **\<Person.Contact>** 元素屬於複雜型別，而且會對應至資料庫中具有相同名稱的資料表。 元素 **\<FirstName>** 和的 [專案名稱] **\<LastName>** 屬性屬於簡單類型，因此會對應到具有相同名稱的資料行。 **EmployeeID** 此範例與先前範例唯一的差別在於，這些元素用於對應 FirstName 和 LastName 欄位。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact">  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="FirstName" type="xsd:string" />   
        <xsd:element name="LastName" type="xsd:string" />   
      </xsd:sequence>  
      <xsd:attribute name="ContactID" type="xsd:integer" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 然後將檔案儲存為 MySchemaElements.xml。  
  
2.  建立下列範本 (MySchemaElementsT.xml)，並將其儲存在先前步驟中所使用的相同目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="MySchemaElements.xml">  
            /Person.Contact  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述指定的目錄路徑是儲存範本之目錄的相對路徑。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchemaElements.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 部分結果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact ContactID="1">  
    <FirstName>Gustavo</FirstName>  
    <LastName>Achong</LastName>  
  </Person.Contact>  
   ...  
</ROOT>  
```  
  
### <a name="c-mapping-an-xml-element-to-an-xml-data-type-column"></a>C. 將 XML 元素對應至 XML 資料類型資料行  
 在此範例中，因為沒有使用註解，因此也會發生預設對應。 **\<Production.ProductModel>** 元素屬於複雜型別，而且會對應至資料庫中具有相同名稱的資料表。 **ProductModelID**屬性屬於簡單類型，因此會對應到具有相同名稱的資料行。 這個專案與先前的範例唯一的差別在於，專案 **\<Instructions>** 會對應至使用該類型的資料行 `xml` `xsd:anyType` 。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Instructions" type="xsd:anyType" />   
      </xsd:sequence>  
      <xsd:attribute name="ProductModelID" type="xsd:integer" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 `xml` 資料類型是在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中導入。  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 MySchemaXmlAnyElements.xml。  
  
2.  建立下列範本 (MySchemaXmlAnyElementsT.xml)，並將其儲存在先前步驟中所使用的相同目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="MySchemaXmlAnyElements.xml">  
            /Production.ProductModel[@ProductModelID=7]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述指定的目錄路徑是儲存範本之目錄的相對路徑。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchemaXmlAnyElements.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 部分結果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductModel ProductModelID="7">  
    <Instructions>  
      <root xmlns="http:  
//schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstru  
ctions">  
...  
      </root>  
    <Instructions>  
  </Production.ProductModel>  
</ROOT>  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的批註式架構安全性考慮](../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [XML 資料 &#40;SQL Server&#41;](../xml/xml-data-sql-server.md)   
 [xml 資料類型在 SQLXML 4.0 中的支援](../sqlxml/xml-data-type-support-in-sqlxml-4-0.md)  
  
  
