---
title: FORMATED_VALUE 上的語言和 FORMAT_STRING |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7534ff5f-954e-47d4-a2ed-4b5b8ccb30e6
author: minewiskan
ms.author: owend
ms.openlocfilehash: ba4aacbbd440da6048680054771c86c40ef96daa
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584757"
---
# <a name="language-and-format_string-on-formated_value"></a>FORMATED_VALUE 上的 LANGUAGE 及 FORMAT_STRING
  FORMATTED_VALUE 屬性是根據資料格中 VALUE、FORMAT_STRING 和 LANGUAGE 屬性的互動而建立。 本主題將說明這些屬性如何互動，以便建立 FORMATTED_VALUE 屬性。  
  
## <a name="value-format_string-language-properties"></a>VALUE、FORMAT_STRING、LANGUAGE 屬性  
 下表說明這些屬性為何，讓您準備一起使用這些屬性。  
  
 值  
 未格式化的資料格值。  
  
 FORMAT_STRING  
 要套用至資料格值來產生 FORMATTED_VALUE 屬性的格式化範本。  
  
 LANGUAGE  
 要沿著 FORMAT_STRING 套用來產生當地語系化 FORMATTED_VALUE 版本的地區設定規格。  
  
## <a name="formatted_value-constructed"></a>建構的 FORMATTED_VALUE  
 FORMATTED_VALUE 屬性的建構方式是利用 VALUE 屬性中的值，以及將 FORMAT_STRING 屬性中指定的格式範本套用到該值。 此外，每當格式值是 `named formatting literal` 時，LANGUAGE 屬性規格就會修改 FORMAT_STRING 的輸出，以遵循具名格式的語言使用方式。 具名格式常值全都是以可當地語系化的方式來定義。 例如， `"General Date"` 是一種可以當地語系化的規格，與下列範本 `"YYYY-MM-DD hh:nn:ss",` 相反，後者指出日期是以範本定義的方式呈現，不論語言規格為何。  
  
 如果 FORMAT_STRING 範本與 LANGUAGE 規格之間有衝突，FORMAT_STRING 範本會覆寫 LANGUAGE 規格。 例如，如果 FORMAT_STRING="$ #0" 且 LANGUAGE=1034 (西班牙)，而且 VALUE=123.456 然後 FORMATTED_VALUE="$ 123" 而非 FORMATTED_VALUE="€ 123"，則預期的格式會是歐元，因為格式範本的值會覆寫指定的語言。  
  
### <a name="examples"></a>範例  
 下列範例示範當搭配 FORMAT_STRING 使用 LANGUAGE 時所取得的輸出。  
  
 第一個範例說明格式化數值，第二個範例說明格式化日期和時間值。  
  
 每一個範例都有提供多維度運算式 (MDX) 程式碼。  
  
 `with`  
  
 `member measures.A as 5040, FORMAT_STRING="Currency"`  
  
 `member measures.B as measures.A, LANGUAGE=1034`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="$#,##0.00"`  
  
 `member measures.D as measures.A, FORMAT_STRING="Scientific"`  
  
 `member measures.E as measures.A, LANGUAGE=1034 , FORMAT_STRING="Scientific"`  
  
 `member measures.F as 0.5040, FORMAT_STRING="Percent"`  
  
 `member measures.G as measures.F, LANGUAGE=1034`  
  
 `member measures.H as 0, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.I as 59, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.J as 0, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `member measures.K as -312, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F, measures.G, measures.H, measures.I, measures.J, measures.K} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 在伺服器上使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 來執行上述 MDX 查詢，而且用戶端的地區設定為 1033 時，調換的結果如下所示：  
  
|成員|FORMATTED_VALUE|說明|  
|------------|----------------------|-----------------|  
|A|$5,040.00|FORMAT_STRING 設定為 `Currency` 而且 LANGUAGE 為 `1033`(從系統地區設定值繼承而來)。|  
|B|5.040,00|FORMAT_STRING 設定為 `Currency` (繼承自 A) 而且 LANGUAGE 明確設定為 `1034` (西班牙)，因此是歐元符號、不同的小數分隔符號和不同的千位分隔符號。|  
|C|$5.040,00|FORMAT_STRING 設定為 `$#,##0.00` (從 A 覆寫貨幣)，而且 LANGUAGE 明確設定為 `1034` (西班牙)。 因為 FORMAT_STRING 屬性明確將貨幣符號設定為 $，所以會使用 $ 符號表示 FORMATTED_VALUE。 但是，因為 `.` (點) 和 `,` (逗號) 分別為小數分隔符號和千位分隔符號的預留位置，所以語言規格會影響它們產生針對小數分隔符號和千位分隔符號所當地語系化的輸出。|  
|D|5.04E+03|FORMAT_STRING 設定為 `Scientific` 而且 LANGUAGE 設定為 `1033`(從系統地區設定值繼承而來)，因此 `.` (點) 是小數分隔符號。|  
|E|5,04E+03|FORMAT_STRING 設定為 `Scientific` 而且 LANGUAGE 明確設定為 `1034,` ，因此 `,` (逗號) 是小數分隔符號。|  
|F|50.40%|FORMAT_STRING 設定為 `Percent` 而且 LANGUAGE 設定為 `1033`(從系統地區設定值繼承而來)，因此 `.` (點) 是小數分隔符號。<br /><br /> 請注意，VALUE 已經從 5040 變更為 0.5040|  
|G|50,40%|FORMAT_STRING 設定為 `Percent`(繼承自 F)，而且 LANGUAGE 明確設定為 `1034` ，因此 `,` (逗號) 是小數分隔符號。<br /><br /> 請注意，VALUE 繼承自 F 值。|  
|H|否|FORMAT_STRING 設定為 `YES/NO`、VALUE 設定為 0 而且 LANGUAGE 明確設定為 `1034`；因為英文 NO 與西班牙 NO 之間沒有任何差異，所以使用者在 FORMATTED_VALUE 中看不到任何差異。|  
|I|SI|FORMAT_STRING 設定為 `YES/NO`、VALUE 設定為 59 而且 LANGUAGE 明確設定為 `1034`；如同針對 YES/NO 格式所定義，因為與零 (0) 不同的任何值都是 YES 而且語言設定為西班牙文，所以 FORMATTED_VALUE 為 SI。|  
|J|Desactivado|FORMAT_STRING 設定為 `ON/OFF`、VALUE 設定為 0 而且 LANGUAGE 明確設定為 `1034`；如同針對 ON/OFF 格式所定義，因為等於零 (0) 的任何值都是 OFF 而且語言設定為西班牙文，所以 FORMATTED_VALUE 為 Desactivado。|  
|K|Activado|FORMAT_STRING 設定為 `ON/OFF`、VALUE 設定為 -312 而且 LANGUAGE 明確設定為 `1034`；如同針對 ON/OFF 格式所定義，因為與零 (0) 不同的任何值都是 ON 而且語言設定為西班牙文，所以 FORMATTED_VALUE 為 Activado。|  
  
 `with`  
  
 `member measures.A as 'CDate("1959-03-12 06:30")'`  
  
 `member measures.B as measures.A, FORMAT_STRING="Long Date"`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="General Date"`  
  
 `member measures.D as measures.A, LANGUAGE=1034, FORMAT_STRING="Long Date"`  
  
 `member measures.E as measures.A, LANGUAGE=1041 , FORMAT_STRING="General Date"`  
  
 `member measures.F as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Date"`  
  
 `member measures.G as measures.A, FORMAT_STRING="Long Time"`  
  
 `member measures.H as measures.A, FORMAT_STRING="Short Time"`  
  
 `member measures.I as measures.A, LANGUAGE=1034 , FORMAT_STRING="Long Time"`  
  
 `member measures.J as measures.A, LANGUAGE=1034 , FORMAT_STRING="Short Time"`  
  
 `member measures.K as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Time"`  
  
 `member measures.L as measures.A, LANGUAGE=1041 , FORMAT_STRING="Short Time"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F`  
  
 `, measures.G, measures.H, measures.I, measures.J, measures.K, measures.L} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 在伺服器上使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 來執行上述 MDX 查詢，而且用戶端的地區設定為 1033 時，調換的結果如下所示：  
  
|成員|FORMATTED_VALUE|說明|  
|------------|----------------------|-----------------|  
|A|3/12/1959 6:30:00 AM|FORMAT_STRING 由 CDate() 運算式隱含地設定為 `General Date` ，而且 LANGUAGE 是 `1033` (英文)，這是從系統地區設定值繼承而來。|  
|B|Thursday, March 12, 1959|FORMAT_STRING 明確設定為 `Long Date` 而且 LANGUAGE 為 `1033` (英文)，這是從系統地區設定值繼承而來。|  
|C|12/03/1959 6:30:00|FORMAT_STRING 明確設定為 `General Date` 且 LANGUAGE 明確設定為 `1034` (西班牙文)。<br /><br /> 請注意，當與美國格式樣式相比較時，就會切換月和日。|  
|D|jueves, 12 de marzo de 1959|FORMAT_STRING 明確設定為 `Long Date` 且 LANGUAGE 明確設定為 `1034` (西班牙文)。<br /><br /> 請注意，月和星期幾是以西班牙文描述。|  
|E|1959/03/12 6:30:00|FORMAT_STRING 明確設定為 `General Date` 且 LANGUAGE 明確設定為 `1041` (日文)。<br /><br /> 請注意，日期現在的格式為：Year/Month/Day Hour:Minutes:Seconds|  
|F|1959年3月12日|FORMAT_STRING 明確設定為 `Long Date` 且 LANGUAGE 明確設定為 `1041` (日文)。|  
|G|6:30:00 AM|FORMAT_STRING 明確設定為 `Long Time` 而且 LANGUAGE 為 `1033` (英文)，這是從系統地區設定值繼承而來。|  
|H|06:30|FORMAT_STRING 明確設定為 `Short Time` 而且 LANGUAGE 為 `1033` (英文)，這是從系統地區設定值繼承而來。|  
|I|6:30:00|FORMAT_STRING 明確設定為 `Long Time` 且 LANGUAGE 明確設定為 `1034` (西班牙文)。|  
|J|06:30|FORMAT_STRING 明確設定為 `Short Time` 且 LANGUAGE 明確設定為 `1034` (西班牙文)。|  
|K|6:30:00|FORMAT_STRING 明確設定為 `Long Time` 且 LANGUAGE 明確設定為 `1041` (日文)。|  
|L|06:30|FORMAT_STRING 明確設定為 `Short Time` 且 LANGUAGE 明確設定為 `1041` (日文)。|  
  
## <a name="see-also"></a>另請參閱  
 [FORMAT_STRING &#40;MDX 的內容&#41;](mdx-cell-properties-format-string-contents.md)   
 [使用資料格屬性 &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)   
 [&#40;MDX&#41;建立和使用屬性值](../../creating-and-using-property-values-mdx.md)   
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
