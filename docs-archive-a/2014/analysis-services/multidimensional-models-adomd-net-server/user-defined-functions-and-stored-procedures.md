---
title: 使用者定義函數和預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- stored procedures [ADOMD.NET]
- ADOMD.NET, user defined functions
- user defined functions [ADOMD.NET]
- ADOMD.NET, UDFs
- ADOMD.NET, stored procedures
ms.assetid: 07e8aa47-37d4-4bbc-8bff-49e422d12897
author: minewiskan
ms.author: owend
ms.openlocfilehash: a49aa41d158bf2c9fd1ebb1a711d6ff35c0df98b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686527"
---
# <a name="user-defined-functions-and-stored-procedures"></a>使用者定義函數和預存程序
  透過 ADOMD.NET 伺服器物件，您可以建立使用者定義函數， (UDF) 或預存程式 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，以便與來自伺服器的中繼資料和資料互動。 這些同處理序 (In-Process) 方法是透過「多維度運算式」(Multidimensional Expressions，MDX) 或「資料採礦延伸模組」(Data Mining Extensions，DMX) 陳述式來呼叫，以提供附加功能，並不會有與網路通訊關聯的延遲。  
  
## <a name="udf-examples"></a>UDF 範例  
 UDF 是一種可以在 MDX 或 DMX 陳述式的內容中呼叫的方法，可以使用任何數目的參數，並且可以傳回任何類型的資料。  
  
 使用 MDX 建立的 UDF 類似於為 DMX 建立的 UDF。 主要的差別在於[microsoft.analysisservices. AdomdServer.](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) coNtext 物件的某些屬性（例如[microsoft.analysisservices. AdomdServer](/previous-versions/sql/sql-server-2014/ms137081(v=sql.120)) ）僅適用于一種指令碼語言或另一種語言版本。 CurrentCube [*](/previous-versions/sql/sql-server-2014/ms137178(v=sql.120))屬性。（英文）。  
  
 下列範例示範如何使用 UDF 傳回節點描述、篩選 Tuple 以及將篩選套用至 Tuple。  
  
### <a name="returning-a-node-description"></a>傳回節點描述  
 下列範例會建立 UDF，以傳回指定節點的節點描述。 UDF 會使用其執行所在的目前內容，並使用 DMX FROM 子句，從目前的採礦模型擷取節點。  
  
```  
public string GetNodeDescription(string nodeUniqueName)  
{  
   return Context.CurrentMiningModel.GetNodeFromUniqueName(nodeUniqueName).Description;  
}  
```  
  
 一旦部署，就可以透過下列 DMX 運算式來呼叫上述 UDF 範例，這將可擷取最有可能的預測節點。 描述包含構成預測節點的條件資訊。  
  
```  
select Cluster(), SampleAssembly.GetNodeDescription( PredictNodeId(Cluster()) ) FROM [Customer Clusters]  
```  
  
### <a name="returning-tuples"></a>傳回 Tuple  
 下列範例使用集合和傳回計數，以及從集合隨機擷取 Tuple，以傳回最後的子集：  
  
```  
public Set RandomSample(Set set, int returnCount)  
{  
   //Return the original set if there are fewer tuples  
   //in the set than the number requested.  
   if (set.Tuples.Count <= returnCount)  
      return set;  
  
   System.Random r = new System.Random();  
   SetBuilder returnSet = new SetBuilder();  
  
   //Retrieve random tuples until the return set is filled.  
   int i = set.Tuples.Count;  
   foreach (Tuple t in set.Tuples)  
   {  
      if (r.Next(i) < returnCount)  
      {  
         returnCount--;  
         returnSet.Add(t);  
      }  
      i--;  
      //Stop the loop if we have enough tuples.  
      if (returnCount == 0)  
         break;  
   }  
   return returnSet.ToSet();  
}  
```  
  
 在下列 MDX 範例中會呼叫上述範例。 在此 MDX 範例中，會從「**艾德公司**」資料庫中取出五個隨機狀態或省份。  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
### <a name="applying-a-filter-to-a-tuple"></a>將篩選套用至 Tuple  
 在下列範例中，UDF 是定義成使用集合，並使用 Expression 物件，將篩選套用至集合中的每個 Tuple。 任何符合篩選的 Tuple 都將加入傳回的集合。  
  
 [!code-csharp[Adomd.NetServer#FilterSet](../../snippets/csharp/SQL14/adomd.net/adomd.netserver/cs/class1.cs#filterset)]  
  
 在下列 MDX 範例中會呼叫上述範例，以便將集合篩選成以 'A' 開頭的城市名稱。  
  
```  
Select Measures.Members on Rows,  
SampleAssembly.FilterSet([Customer].[Customer Geography].[City], "[Customer].[Customer Geography].[City].CurrentMember.Name < 'B'") on Columns  
From [Adventure Works]  
```  
  
## <a name="stored-procedure-example"></a>預存程序範例  
 在下列範例中，以 MDX 為基礎的預存程序使用 AMO 為「網際網路銷售」建立資料分割 (若有需要的話)。  
  
 [!code-csharp[Adomd.NetServer#CreateInternetSalesMeasureGroupPartitions](../../snippets/csharp/SQL14/adomd.net/adomd.netserver/cs/class1.cs#createinternetsalesmeasuregrouppartitions)]  
  
  
