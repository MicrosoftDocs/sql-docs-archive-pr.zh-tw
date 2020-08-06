---
title: 步驟 3：加入錯誤流程重新導向 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ceaea310cba05a940f310c01b52d5f912a53bea8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595178"
---
# <a name="step-3-adding-error-flow-redirection"></a>步驟 3：新增錯誤流程重新導向
  如上一項工作所示範的，當 [查閱貨幣索引鍵] 轉換試圖處理已損毀範例一般檔案 (其產生錯誤) 時，不會產生相符者。 因為轉換使用錯誤輸出的預設值，所以任何錯誤都會造成轉換失敗。 當轉換失敗時，封裝的其餘部分也會失敗。  
  
 若不要讓轉換失敗，您可以設定元件利用錯誤輸出將失敗的資料列重新導向至另一個處理路徑。 使用個別錯誤處理路徑可讓您做一些事。 例如，您可以試著清除資料，然後重新處理失敗的資料列。 或者，您可以儲存失敗的資料列及其他錯誤資訊，供以後驗證及重新處理。  
  
 在這項工作中，您將設定查閱貨幣索引鍵轉換，將失敗的資料列重新導向至錯誤輸出。 在資料流程的錯誤分支中，會將這些資料列寫入檔案。  
  
 根據預設，錯誤輸出中的兩個額外資料行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ： **ErrorCode**和**ErrorColumn**，只包含代表錯誤號碼的數位代碼，以及發生錯誤的資料行識別碼。 這些數值若無對應的錯誤描述，則用途有限。  
  
 為了加強錯誤輸出的有用性，在此封裝將失敗資料列寫至檔案之前，您將使用指令碼元件來存取 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] API 及取得該錯誤的描述。  
  
### <a name="to-configure-an-error-output"></a>設定錯誤輸出  
  
1.  在 [ **SSIS 工具箱**] 中，展開 [**一般**]，然後將 [**腳本元件**] 拖曳**至 [資料流程]** 索引標籤的設計介面上。將 [**腳本**] 放到 [**查閱貨幣索引鍵**] 轉換的右邊。  
  
2.  在 **[選取指令碼元件類型]** 對話方塊中，按一下 **[轉換]**，然後按一下 **[確定]**。  
  
3.  按一下 **[查閱貨幣索引鍵]** 轉換，將紅色箭頭拖曳至新加入的 **[指令碼]** 轉換來連接兩個元件。  
  
     紅色箭頭代表 **[查閱貨幣索引鍵]** 轉換的錯誤輸出。 藉由使用紅色箭頭將轉換連接到指令碼元件，您可以將任何處理錯誤重新導向至指令碼元件，然後由它處理這些錯誤並傳送到目的地。  
  
4.  在 **[設定錯誤輸出]** 對話方塊的 **[錯誤]** 資料行中，選取 **[重新導向資料列]**，然後按一下 **[確定]**。  
  
5.  在 [資料流程]**** 設計介面中，於新加入的 **ScriptComponent** 中按一下 [指令碼元件]****，將名稱變更為**取得錯誤描述**。  
  
6.  按兩下 [取得錯誤描述]**** 轉換。  
  
7.  在 **[指令碼轉換編輯器]** 對話方塊的 **[輸入資料行]** 頁面上，選取 **[ErrorCode]** 資料行。  
  
8.  在 **[輸入和輸出]** 頁面，展開 **[Output 0]**，按一下 **[輸出資料行]**，然後按一下 **[加入資料行]**。  
  
9. 在 `Name` 屬性中，輸入**ErrorDescription** ，並將 `DataType` 屬性設定為 **[Unicode 字串 [DT_WSTR]]**。  
  
10. 在 [**腳本**] 頁面上，確認 `LocaleID` 屬性已設為 [**英文] ([美國]。**  
  
11. 按一下 [編輯指令碼]**** 以開啟 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA)。 在 `Input0_ProcessInputRow` 方法中，輸入或剖析下列程式碼。  
  
     [Visual Basic]  
  
    ```  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
     [Visual C#]  
  
    ```  
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
     完成的副程式類似下列程式碼。  
  
     [Visual Basic]  
  
    ```  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
     [Visual C#]  
  
    ```  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. 在 **[建置]** 功能表上，按一下 **[建置方案]** 建置指令碼並儲存您的變更，然後關閉 VSTA。  
  
13. 按一下 **[確定]** 來關閉 **[指令碼轉換編輯器]** 對話方塊。  
  
## <a name="next-steps"></a>後續步驟  
 [步驟4：新增一般檔案目的地] (lesson-4-4-adding-a-flat-file-destination.md  
  
  
