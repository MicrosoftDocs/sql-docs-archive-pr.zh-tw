---
title: FOR XML 子句的基本語法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- BINARY BASE64 directive
- ROOT directive
- FOR XML clause, BINARY BASE64 directive
- FOR XML clause, syntax
- FOR XML clause, ROOT directive
ms.assetid: df19ecbf-d28e-4e9c-aaa3-700f8bbd3be4
author: rothja
ms.author: jroth
ms.openlocfilehash: dc0410e7a54674673f64442d8a3cf9476d250033
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585193"
---
# <a name="basic-syntax-of-the-for-xml-clause"></a>FOR XML 子句的基本語法
  FOR XML 模式可以是 RAW、AUTO、EXPLICIT 或 PATH。 它可以決定產生 XML 的外觀。  
  
> [!IMPORTANT]  
>  FOR XML 選項的 XMLDATA 指示詞已被取代。 在 RAW 和 AUTO 模式的情況下，請使用 XSD 產生。 EXPLICT 模式中沒有 XMLDATA 指示詞的替代項目。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 以下是[FOR 子句 (transact-sql) ](/sql/t-sql/queries/select-for-clause-transact-sql)中所述的基本語法：  
  
```  
[ FOR { BROWSE | <XML> } ]  
<XML> ::=  
XML   
    {   
      { RAW [ ('ElementName') ] | AUTO }   
        [   
           <CommonDirectives>   
           [ , { XMLDATA | XMLSCHEMA [ ('TargetNameSpaceURI') ]} ]   
           [ , ELEMENTS [ XSINIL | ABSENT ]   
        ]  
      | EXPLICIT   
        [   
           <CommonDirectives>   
           [ , XMLDATA ]   
        ]  
      | PATH [ ('ElementName') ]   
        [   
           <CommonDirectives>   
           [ , ELEMENTS [ XSINIL | ABSENT ] ]  
        ]  
     }   
  
 <CommonDirectives> ::=   
   [ , BINARY BASE64 ]  
   [ , TYPE ]  
   [ , ROOT [ ('RootName') ] ]  
```  
  
## <a name="arguments"></a>引數  
 RAW[('*ElementName*')]  
 使用查詢結果並將結果集中的每一個資料列轉換為 XML 元素，該元素包含作為元素標記的泛用識別碼 \<row />。 當您使用此指示詞時，您可以選擇性地指定資料列元素的名稱。 產生的 XML 將會使用指定的 *ElementName* 作為針對每個資料列所產生的資料列元素。 如需詳細資訊，請參閱 [搭配 FOR XML 使用 RAW 模式](use-raw-mode-with-for-xml.md)。  
  
 AUTO  
 將查詢結果以簡易巢狀 XML 樹狀結構傳回。 FROM 子句中的每個資料表至少都有一個資料行是列在 SELECT 子句中，這些資料表是以 XML 元素表示。 列在 SELECT 子句中的資料行會對應到適當的元素屬性。 如需詳細資訊，請參閱 [搭配 FOR XML 使用 AUTO 模式](use-auto-mode-with-for-xml.md)。  
  
 EXPLICIT  
 指定產生之 XML 樹狀結構的形狀已明確地定義。 透過使用此模式，必須以特定方式撰寫查詢，這樣才能明確地指定您需要的巢狀其他資訊。 如需詳細資訊，請參閱 [搭配 FOR XML 使用 EXPLICIT 模式](use-explicit-mode-with-for-xml.md)。  
  
 PATH  
 提供更簡單的方式來混合元素與屬性，並引用其他的巢狀來代表複雜的屬性。 您可以使用 FOR XML EXPLICIT 模式查詢來建構從資料列集而來的這類 XML，但是 PATH 模式對於可能會比較繁雜的 EXPLICIT 模式查詢提供較簡單的替代方案。 PATH 模式還可撰寫巢狀 FOR XML 查詢及 TYPE 指示詞，以傳回 **xml** 類型執行個體，這將可讓您撰寫較不複雜的查詢。 它為撰寫大部份的 EXPLICIT 模式查詢提供替代方案。 根據預設，PATH 模式會針對結果集中的每個資料列產生 \<row> 元素包裝函式。 您可以選擇性地指定元素名稱。 如果您有選擇，則會將指定名稱做為包裝函數的元素名稱。 如果您提供空白字串 (FOR XML PATH (''))，就不會產生包裝函數元素。 如需詳細資訊，請參閱 [搭配 FOR XML 使用 PATH 模式](use-path-mode-with-for-xml.md)。  
  
 XMLDATA  
 指定應傳回的內嵌 XML-Data Reduced (XDR) 結構描述。 結構描述則是文件預先決定的內嵌結構描述。 如需實用範例，請參閱 [搭配 FOR XML 使用 RAW 模式](use-raw-mode-with-for-xml.md)。  
  
 XMLSCHEMA  
 傳回內嵌 W3C XML 結構描述 (XSD)。 在指定此指示詞時，您可以選擇性地指定目標命名空間 URI。 這將會傳回結構描述中指定的命名空間。 如需詳細資訊，請參閱 [產生內嵌 XSD 結構描述](generate-an-inline-xsd-schema.md)。 如需實用範例，請參閱 [搭配 FOR XML 使用 RAW 模式](use-raw-mode-with-for-xml.md)。  
  
 ELEMENTS  
 若指定了 ELEMENTS 選項，則資料行會以子元素傳回。 否則這些資料行會對應到 XML 屬性。 此選項只在 RAW、AUTO 以及 PATH 模式中才有支援。 在使用此指示詞時，您可以選擇性地指定 XSINIL 或 ABSENT。 XSINIL 可指定將含有 **xsi:nil** 屬性的元素，設為針對 NULL 資料行值所建立的 True。 依預設或當同時指定 ABSENT 與 ELEMENTS 時，就不會針對 NULL 值建立任何元素。 如需實用範例，請參閱 [搭配 FOR XML 使用 RAW 模式](use-raw-mode-with-for-xml.md) 和 [搭配 FOR XML 使用 AUTO 模式](use-auto-mode-with-for-xml.md)。  
  
 BINARY BASE64  
 若指定 BINARY Base64 選項，則任何由查詢所傳回的二進位資料都會以 base64 編碼格式表示。 若要使用 RAW 和 EXPLICIT 模式擷取二進位資料，必須指定此選項。 在 AUTO 模式下，二進位資料在預設下是以參考來傳回。 如需實用範例，請參閱 [搭配 FOR XML 使用 RAW 模式](use-raw-mode-with-for-xml.md)。  
  
 TYPE  
 指定查詢以 **xml** 類型傳回結果。 如需詳細資訊，請參閱 [FOR XML 查詢中的 TYPE 指示詞](type-directive-in-for-xml-queries.md)。  
  
 ROOT [('*RootName*')]  
 指定將單一最上層元素加入產生的 XML。 您可以選擇性地指定要產生的根元素名稱。 預設值是 "root"。  
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR XML 的 RAW 模式](use-raw-mode-with-for-xml.md)   
 [搭配 FOR XML 使用 AUTO 模式](use-auto-mode-with-for-xml.md)   
 [搭配 FOR XML 使用 EXPLICIT 模式](use-explicit-mode-with-for-xml.md)   
 [搭配 FOR XML 使用 PATH 模式](use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
