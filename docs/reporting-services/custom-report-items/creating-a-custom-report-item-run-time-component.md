---
title: 사용자 지정 보고서 항목 런타임 구성 요소 만들기 | Microsoft Docs
description: 사용자 지정 보고서 항목 런타임 구성 요소를 만들고 디자인 환경에서 이 구성 요소의 속성을 정의하는 방법을 알아봅니다.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items, creating
ms.assetid: b3e15a4a-98f8-4dbb-b847-bbcb20327051
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0946739b0b0aaefd1e0d6a682f0228dfa98529c9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80216987"
---
# <a name="creating-a-custom-report-item-run-time-component"></a>사용자 지정 보고서 항목 런타임 구성 요소 만들기
  사용자 지정 보고서 항목 런타임 구성 요소는 CLS 규격 언어를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 구성 요소로 구현되며 런타임에 보고서 처리기에 의해 호출됩니다. 사용자 지정 보고서 항목의 해당 디자인 타임 구성 요소를 수정하여 디자인 환경에서 런타임 구성 요소에 대한 속성을 정의합니다.  
  
 완전히 구현된 사용자 지정 보고서 항목 예는 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="definition-and-instance-objects"></a>정의 및 인스턴스 개체  
 사용자 지정 보고서 항목을 구현하기 전에 *정의 개체*와 *인스턴스 개체*의 차이점을 알아야 합니다. 정의 개체는 사용자 지정 보고서 항목의 RDL 표현을 제공하고, 인스턴스 개체는 정의 개체의 평가된 버전입니다. 보고서의 각 항목에 정의 개체는 하나만 있습니다. 식이 포함된 정의 개체의 속성에 액세스할 때 사용자는 평가되지 않은 식 문자열을 받습니다. 인스턴스 개체는 정의 개체의 평가된 버전을 포함하고 항목의 정의 개체와 일 대 다 관계를 맺을 수 있습니다. 예를 들어, 보고서의 정보 행에 <xref:Microsoft.ReportingServices.OnDemandReportRendering.Tablix>이 포함된 <xref:Microsoft.ReportingServices.OnDemandReportRendering.CustomReportItem> 데이터 영역이 있는 경우 정의 개체는 하나뿐이지만 인스턴스 개체는 데이터 영역의 각 행마다 있습니다.  
  
## <a name="implementing-the-icustomreportitem-interface"></a>ICustomReportItem 인터페이스 구현  
 **CustomReportItem** 런타임 구성 요소를 만들려면 Microsoft.ReportingServices.ProcessingCore.dll에 정의된 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem> 인터페이스를 구현해야 합니다.  
  
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
  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem> 인터페이스를 구현한 후에는 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> 및 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A> 메서드 스텁이 생성됩니다. <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> 메서드가 먼저 호출되어, 정의 속성을 설정하고 이 정의 속성과 항목 렌더링에 사용되는 인스턴스 속성을 포함할 <xref:Microsoft.ReportingServices.OnDemandReportRendering.Image> 개체를 만듭니다. 정의 개체가 평가된 후 <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A> 메서드가 호출되고, 항목 렌더링에 사용되는 인스턴스 개체를 제공합니다.  
  
 다음은 컨트롤 이름을 이미지로 렌더링하는 사용자 지정 보고서 항목의 예제 구현입니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 보고서 항목 아키텍처](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [사용자 지정 보고서 항목 디자인 타임 구성 요소 만들기](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [사용자 지정 보고서 항목 클래스 라이브러리](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [방법: 사용자 지정 보고서 항목 배포](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
