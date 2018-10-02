---
title: Detail 속성을 사용하여 특정 오류 처리 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4aebb8febbf181a54ed32f31096c408c04c1dae3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621991"
---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>Detail 속성을 사용하여 특정 오류 처리
  예외를 상세하게 분류하기 위해 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 SOAP 예외의 **Detail** 속성에서 자식 요소의 **InnerText** 속성으로 추가 오류 정보를 반환합니다. **Detail** 속성은 **XmlNode** 개체이므로 다음 코드를 사용하여 **Message** 자식 요소의 내부 텍스트에 액세스할 수 있습니다.  
  
 **Detail** 속성에 포함된 사용 가능한 모든 자식 요소 목록은 [Detail 속성](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)을 참조하세요. 자세한 내용은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 설명서의 "Detail 속성(Detail Property)"을 참조하세요.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [SoapException 오류 테이블](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
