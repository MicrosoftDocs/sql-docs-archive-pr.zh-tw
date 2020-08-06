---
title: 建立自訂報表項目執行階段元件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, creating
ms.assetid: b3e15a4a-98f8-4dbb-b847-bbcb20327051
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 50c5c0211bc5cd1359af9d1493782bd9d96c2b3a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585157"
---
# <a name="creating-a-custom-report-item-run-time-component"></a>建立自訂報表項目執行階段元件
  自訂報表專案執行時間元件會 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 使用任何符合 CLS 標準的語言實作為元件，並在執行時間由報表處理器呼叫。 您可藉由修改自訂報表項目對應的設計階段元件，在設計環境中定義執行階段元件的屬性。  

<!--
Replacing the following multiValue.....

ms.technology: 
  - "docset-sql-devref"
  - "reporting-services-native"

.....with the following single value.....

ms.technology: reporting-services
.

(GeneMi = MightyPen  ,  2019-04-20  ,  DevO= 1515083)
-->

 如需完全實作的自訂報表項目的範例，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="definition-and-instance-objects"></a>定義和執行個體物件  
 在實作自訂報表項目之前，了解「定義物件」** 和「執行個體物件」** 之間的差異很重要。 定義物件提供自訂報表項目的 RDL 表示法，而執行個體物件是定義物件的評估版本。 報表上每個項目只有一個定義物件。 在包含運算式的定義物件上存取屬性時，您會取得未評估過的運算式字串。 執行個體物件包含已評估的定義物件版本，而且與項目的定義物件可能具有一對多的關聯性。 例如，如果報表具有 <xref:Microsoft.ReportingServices.OnDemandReportRendering.Tablix> 資料區，而該資料區在詳細資料列中包含 <xref:Microsoft.ReportingServices.OnDemandReportRendering.CustomReportItem>，則只會有一個定義物件，但資料區中的每個資料列都會有一個執行個體物件。  
  
## <a name="implementing-the-icustomreportitem-interface"></a>實作 ICustomReportItem 介面  
 若要建立 `CustomReportItem` 執行階段元件，您需要實作定義於 Microsoft.ReportingServices.ProcessingCore.dll 的 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem> 介面：  
  
```csharp  
namespace Microsoft.ReportingServices.OnDemandReportRendering  
{  
    public interface ICustomReportItem  
    {  
        void GenerateReportItemDefinition(CustomReportItem customReportItem);  
void EvaluateReportItemInstance(CustomReportItem customReportItem);  
    }  
}  
```  
  
 在實作 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem> 介面之後，將為您產生兩個方法 Stub：<xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> 和 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A>。 系統會先呼叫 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> 方法，並用它來設定定義屬性及建立 <xref:Microsoft.ReportingServices.OnDemandReportRendering.Image> 物件，此物件將同時包含用於轉譯項目的定義屬性和執行個體屬性。 在評估定義物件之後會呼叫 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A> 方法，這個方法提供用於轉譯項目的執行個體物件。  
  
 以下是自訂報表項目的範例實作，此實作會將控制項的名稱轉譯為影像。  
  
```csharp  
namespace Microsoft.Samples.ReportingServices  
{  
    using System;  
    using System.Collections.Generic;  
    using System.Collections.Specialized;  
    using System.Drawing.Imaging;  
    using System.IO;  
    using System.Text;  
    using Microsoft.ReportingServices.OnDemandReportRendering;  
  
    public class PolygonsCustomReportItem : ICustomReportItem  
    {  
        #region ICustomReportItem Members  
  
        public void GenerateReportItemDefinition(CustomReportItem cri)  
        {  
            // Create the Image object that will be   
            // used to render the custom report item  
            cri.CreateCriImageDefinition();  
            Image polygonImage = (Image)cri.GeneratedReportItem;  
        }  
  
        public void EvaluateReportItemInstance(CustomReportItem cri)  
        {  
            // Get the Image definition  
            Image polygonImage = (Image)cri.GeneratedReportItem;  
  
            // Create the image for the custom report item  
            polygonImage.ImageInstance.ImageData = DrawImage(cri);  
        }  
  
        #endregion  
  
        /// <summary>  
        /// Creates an image of the CustomReportItem's name  
        /// </summary>  
        private byte[] DrawImage(CustomReportItem customReportItem)  
        {  
            int width = 1;          // pixels  
            int height = 1;         // pixels  
            int resolution = 75;    // dpi  
  
            System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap(width, height);  
            bitmap.SetResolution(resolution, resolution);  
  
            System.Drawing.Graphics graphics = System.Drawing.Graphics.FromImage(bitmap);  
            graphics.PageUnit = System.Drawing.GraphicsUnit.Pixel;  
  
            // Get the Font for the Text  
            System.Drawing.Font font = new System.Drawing.Font(System.Drawing.FontFamily.GenericMonospace,  
                12, System.Drawing.FontStyle.Regular);  
  
            // Get the Brush for drawing the Text  
            System.Drawing.Brush brush = new System.Drawing.SolidBrush(System.Drawing.Color.LightGreen);  
  
            // Get the measurements for the image  
            System.Drawing.SizeF maxStringSize = graphics.MeasureString(customReportItem.Name, font);  
            width = (int)(maxStringSize.Width + 2 * font.GetHeight(resolution));  
            height = (int)(maxStringSize.Height + 2 * font.GetHeight(resolution));  
  
            bitmap.Dispose();  
            bitmap = new System.Drawing.Bitmap(width, height);  
            bitmap.SetResolution(resolution, resolution);  
  
            graphics.Dispose();  
            graphics = System.Drawing.Graphics.FromImage(bitmap);  
            graphics.PageUnit = System.Drawing.GraphicsUnit.Pixel;  
  
            // Draw the text  
            graphics.DrawString(customReportItem.Name, font, brush, font.GetHeight(resolution),   
                font.GetHeight(resolution));  
  
            // Create the byte array of the image data  
            MemoryStream memoryStream = new MemoryStream();  
            bitmap.Save(memoryStream, ImageFormat.Bmp);  
            memoryStream.Position = 0;  
            byte[] imageData = new byte[memoryStream.Length];  
            memoryStream.Read(imageData, 0, imageData.Length);  
  
            return imageData;  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [自訂報表專案架構](custom-report-item-architecture.md)   
 [建立自訂報表專案設計階段元件](creating-a-custom-report-item-design-time-component.md)   
 [自訂報表專案類別庫](custom-report-item-class-libraries.md)   
 [操作說明：部署自訂報表項目](how-to-deploy-a-custom-report-item.md)  
  
  
