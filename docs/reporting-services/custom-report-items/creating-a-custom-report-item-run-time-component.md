---
title: "カスタム レポート アイテムの実行時コンポーネントの作成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, creating
ms.assetid: b3e15a4a-98f8-4dbb-b847-bbcb20327051
caps.latest.revision: 33
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5ff245d02fd83794ac61f82e90ff2b48b96259d8
ms.contentlocale: ja-jp
ms.lasthandoff: 06/13/2017

---
# <a name="creating-a-custom-report-item-run-time-component"></a>カスタム レポート アイテムの実行時コンポーネントの作成
  としてカスタム レポート アイテムの実行時コンポーネントが実装されている、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLS 準拠の言語を使用して、コンポーネントとは、レポート プロセッサによって実行時に呼び出されます。 実行時コンポーネントのプロパティをデザイン環境で定義するには、カスタム レポート アイテムの対応するデザイン時コンポーネントを変更します。  
  
 完全に実装されたカスタム レポート アイテムのサンプルについては、次を参照してください。 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)です。  
  
## <a name="definition-and-instance-objects"></a>定義オブジェクトおよびインスタンス オブジェクト  
 カスタム レポート アイテムを実装する前にすることが重要の違いを理解*定義オブジェクト*と*インスタンス オブジェクト*です。 定義オブジェクトはカスタム レポート アイテムの RDL 表記を提供するのに対し、インスタンス オブジェクトは定義オブジェクトの評価されたバージョンです。 定義オブジェクトは、レポートの各アイテムに 1 つしか存在しません。 定義オブジェクトのプロパティのうち、式が含まれたプロパティにアクセスすると、評価されていない式の文字列を取得します。 インスタンス オブジェクトには定義オブジェクトの評価されたバージョンが含まれるので、インスタンス オブジェクトはアイテムの定義オブジェクトと一対多のリレーションシップを持つことができます。 たとえば、詳細行に <xref:Microsoft.ReportingServices.OnDemandReportRendering.Tablix> を含む <xref:Microsoft.ReportingServices.OnDemandReportRendering.CustomReportItem> データ領域がレポートにある場合、定義オブジェクトは 1 つしか存在しませんが、インスタンス オブジェクトはデータ領域の各行に存在します。  
  
## <a name="implementing-the-icustomreportitem-interface"></a>ICustomReportItem インターフェイスの実装  
 作成する、 **CustomReportItem**実行時コンポーネントを実装する必要があります、 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem> Microsoft.ReportingServices.ProcessingCore.dll で定義されているインターフェイス。  
  
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
  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem> インターフェイスを実装すると、<xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> および <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A> という 2 つのメソッド スタブが生成されます。 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> メソッドが最初に呼び出され、定義プロパティの設定と <xref:Microsoft.ReportingServices.OnDemandReportRendering.Image> オブジェクトの作成に使用されます。このオブジェクトには、アイテムの表示に使用される定義プロパティとインスタンス プロパティの両方が含まれます。 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A> メソッドは、定義オブジェクトの評価後に呼び出され、アイテムの表示に使用されるインスタンス オブジェクトを提供します。  
  
 次に、コントロール名をイメージとして表示するカスタム レポート アイテムの実装例を示します。  
  
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
  
## <a name="see-also"></a>参照  
 [カスタム レポート アイテムのアーキテクチャ](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [カスタム レポート アイテムのデザイン時コンポーネントの作成](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [カスタム レポート アイテムのクラス ライブラリ](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [カスタム レポート アイテムを配置する方法](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  