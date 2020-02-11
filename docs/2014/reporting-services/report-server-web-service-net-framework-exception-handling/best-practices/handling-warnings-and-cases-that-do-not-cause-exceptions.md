---
title: 예외를 발생하지 않는 경고 및 사례 처리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], warnings that don't cause
- warnings [Reporting Services]
ms.assetid: 475c0713-6265-44e7-9ebc-ebdd1b89e0af
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4c2c58a5edf42966ba828288c2aa8b84dbb49967
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046105"
---
# <a name="handling-warnings-and-cases-that-do-not-cause-exceptions"></a>예외를 발생하지 않는 경고 및 사례 처리
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 경고 및 특정 오류에 대해 예외를 throw하지 않습니다. 예를 들어 <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> 메서드를 사용하여 새 보고서를 보고서 서버에 게시하는 경우 발생하는 경고는 <xref:ReportService2010.Warning> 개체의 배열의 형태로 반환됩니다. 이러한 경고는 적절한 조치를 취할 수 있도록 처리되고 표시되어야 합니다.  
  
```vb  
Try  
   rs.CreateCatalogItem(name, parentFolder, False, definition, Nothing, warnings)  
  
   If Not (warnings.Length = 0) Then  
      Dim warning As Warning  
      For Each warning In warnings  
         Console.WriteLine(warning.Message)  
      Next warning  
   Else  
      Console.WriteLine("Report {0} created successfully with no warnings", name)  
   End If  
  
Catch ex As SoapException  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.CreateCatalogItem("Report", name, parentFolder, false, definition, null, out warnings);  
  
   if (warnings.Length != 0)  
   {  
      foreach (Warning warning in warnings)  
      {  
         Console.WriteLine(warning.Message);  
      }  
   }  
   else  
      Console.WriteLine("Report {0} created successfully with no warnings", name);  
}  
  
catch (SoapException ex)  
{  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
 오류를 처리하는 또 하나의 방법은 특정 메서드의 반환 값을 평가하는 것입니다. 예를 들어 <xref:ReportService2010.ReportingService2010.FindItems%2A> 메서드를 사용하여 보고서 서버 데이터베이스의 특정 항목을 검색할 수 있습니다. 검색 조건과 일치하는 항목을 찾지 못할 경우 <xref:ReportService2010.CatalogItem> 개체의 null 배열이 반환됩니다. 발견된 항목이 없는 경우 배열을 평가하고 `null`인지 확인한 후 사용자에게 알려야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:ReportService2010.CatalogItem>   
 [Reporting Services의 예외 처리 소개](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../soapexception-class/reporting-services-soapexception-class.md)  
  
  
