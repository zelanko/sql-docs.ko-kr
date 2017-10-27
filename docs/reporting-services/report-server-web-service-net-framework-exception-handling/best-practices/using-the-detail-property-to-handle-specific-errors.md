---
title: "Detail 속성을 사용 하 여 특정 오류 처리 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cbbaf57ce4726bbb16c8cb722f50ac186fe59d81
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>Detail 속성을 사용하여 특정 오류 처리
  예외를 상세하게 분류 하기 위해 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 에서 추가 오류 정보를 반환는 **InnerText** SOAP 예외에서 자식 요소의 속성 **세부** 속성입니다. 때문에 **세부** 속성은 한 **XmlNode** 개체의 내부 텍스트에 액세스할 수 있습니다는 **메시지** 다음 코드를 사용 하 여 자식 요소입니다.  
  
 모든 사용 가능한 자식 요소에 포함 된 목록은 **세부** 속성 참조 [Detail 속성](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)합니다. 자세한 내용은의 "Detail 속성" 참조는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 설명서입니다.  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   ' The exception is a SOAP exception, so use  
   ' the Detail property's Message element.  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   // The exception is a SOAP exception, so use  
   // the Detail property's Message element.  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   If ex.Detail("ErrorCode").InnerXml = "rsInvalidItemName" Then  
   End If ' Perform an action based on the specific error code  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   if (ex.Detail["ErrorCode"].InnerXml == "rsInvalidItemName")  
   {  
      // Perform an action based on the specific error code  
   }  
}  
```  
  
 다음 코드 줄은 SOAP 예외로 콘솔에 반환되는 특정 오류 코드를 작성합니다. 오류 코드를 평가하고 특정 동작을 수행할 수도 있습니다.  
  
```vb  
Console.WriteLine(ex.Detail("ErrorCode").InnerXml)  
```  
  
```csharp  
Console.WriteLine(ex.Detail["ErrorCode"].InnerXml);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [SoapException 오류 테이블](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  

