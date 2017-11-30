---
title: "배달 확장 프로그램에 대해 IDeliveryReportServerInformation 인터페이스 사용 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9f1acb146323a301d90c5c4f4ac1df6fd5b477d6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>배달 확장 프로그램에 대해 IDeliveryReportServerInformation 인터페이스 사용
  <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 인터페이스는 보고서 서버에 대한 정보를 검색하는 데 사용할 수 있는 여러 가지 속성을 표시합니다. 이 정보를 사용하여 알림 및 보고서를 배달할 수 있습니다. 배달 확장 프로그램 클래스를 구현하는 경우 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 인터페이스에서 필요한 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 속성을 구현합니다. <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 속성은 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 인터페이스를 구현하는 개체를 반환합니다. 이 개체로부터 보고서 서버에서 현재 지원하는 렌더링 확장 프로그램 목록을 구할 수 있습니다.  
  
 다음 **for** 루프를 사용하여 보고서 서버의 **ArrayList** 개체에서 현재 사용 가능한 렌더링 확장 프로그램 목록을 저장할 수 있습니다.  
  
```vb  
Dim renderFormats As New ArrayList()  
Dim e As Microsoft.ReportingServices.Interfaces.Extension  
For Each e In  ReportServerInformation.RenderingExtension  
   If e.Visible Then  
      renderFormats.Add(e.Name)  
   End If  
Next e  
```  
  
```csharp  
ArrayList renderFormats = new ArrayList();  
foreach (Microsoft.ReportingServices.Interfaces.Extension e in ReportServerInformation.RenderingExtension)  
{   
   if (e.Visible)  
   {  
      renderFormats.Add(e.Name);  
   }  
}  
```  
  
 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 인터페이스에 대한 자세한 내용은 [배달 확장 프로그램에 대해 IDeliveryReportServerInformation 인터페이스 사용](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
