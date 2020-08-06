---
title: 第3課：從報表伺服器載入報表定義 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ad8b31c-43b0-4481-a31b-090cbed4a438
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: dc6ed26703599792b9c739f8d185ae4f190fc8be
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594882"
---
# <a name="lesson-3-load-a-report-definition-from-the-report-server"></a>第 3 課：從報表伺服器載入報表定義
  在您建立專案並從 RDL 結構描述產生類別之後，就可以開始從報表伺服器載入報表定義。  
  
### <a name="to-load-a-report-definition"></a>載入報表定義  
  
1.  `ReportUpdater`如果您使用類別的) ，請在類別 (模組的頂端新增私用欄位 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] `Report` 。 此欄位將用來在應用程式使用期間，維護從報表伺服器載入的報表參考。  
  
    ```csharp  
    private Report _report;  
    ```  
  
    ```vb  
    Private m_report As Report  
    ```  
  
2.  以下列程式碼取代 Program.cs 檔案 (在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中為 Module1.vb) 中 `LoadReportDefinition()` 方法的程式碼：  
  
    ```csharp  
    private void LoadReportDefinition()  
    {  
        System.Console.WriteLine("Loading Report Definition");  
  
        string reportPath =   
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012";  
  
        // Retrieve the report definition   
        // from the report server  
        byte[] bytes =   
            _reportService.GetItemDefinition(reportPath);  
  
        if (bytes != null)  
        {  
            XmlSerializer serializer =   
                new XmlSerializer(typeof(Report));  
  
            // Load the report bytes into a memory stream  
            using (MemoryStream stream = new MemoryStream(bytes))  
            {  
                // Deserialize the report stream to an   
                // instance of the Report class  
                _report = (Report)serializer.Deserialize(stream);  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub LoadReportDefinition()  
  
        System.Console.WriteLine("Loading Report Definition")  
  
        Dim reportPath As String = _  
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012"  
  
        'Retrieve the report definition   
        'from the report server  
        Dim bytes As Byte() = _  
            m_reportService.GetItemDefinition(reportPath)  
  
        If Not (bytes Is Nothing) Then  
  
            Dim serializer As XmlSerializer = _  
                New XmlSerializer(GetType(Report))  
  
            'Load the report bytes into a memory stream  
            Using stream As MemoryStream = New MemoryStream(bytes)  
  
                'Deserialize the report stream to an   
                'instance of the Report class  
                m_report = CType(serializer.Deserialize(stream), _  
                                 Report)  
  
            End Using  
  
        End If  
  
    End Sub  
    ```  
  
## <a name="next-lesson"></a>下一課  
 在下一課，您將撰寫程式碼，更新從報表伺服器載入的報表定義。 請參閱[第4課：以程式設計方式更新報表定義](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用從 RDL 架構產生的類別更新報表 &#40;SSRS 教學課程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [報表定義語言 &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
