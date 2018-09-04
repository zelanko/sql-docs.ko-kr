---
title: HelpLink 요소 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c1c7dc8cc5104c05afc28fbf0dd74602d66fd682
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280162"
---
# <a name="helplink-element"></a>HelpLink 요소
  **Detail** 속성의 **HelpLink** 요소는 보고서 서버에서 생성되는 URL 문자열입니다. 이 URL은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 도움말 및 지원에서 관리되는 웹 페이지를 대상으로 하며 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 발생하는 특정 오류에 대한 추가 도움말 및 기술 자료 문서를 제공합니다. URL의 구문은 다음과 같습니다.  
  
 **http://** www.microsoft.com**/** products**/** ee**/** transform.aspx **?EvtSrc**=v*alue***&EvtID**=* value ***&ProdName**=* value***&ProdVer**=* value*  
  
 다음 표는 **HelpLink** URL의 인수를 나열합니다.  
  
|인수|값|  
|--------------|-----------|  
|**EvtSrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**EvtID**|보고서 서버 오류 코드입니다(예: rsReservedItem).|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services". 제품 이름 값은 URL로 인코딩됩니다.|  
|**ProdVer**|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 버전 번호입니다. "8.00"은 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]를 나타냅니다.|  
  
 다음 예는 오류 코드 **rsReservedItem**에 대해 반환되는 **HelpLink** URL을 보여 줍니다. 이 오류는 사용자가 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 예약된 항목을 수정하거나 삭제하려고 시도할 때 발생합니다.  
  
```  
http://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 코드의 **HelpLink** 요소는 **SoapException** 클래스를 사용하여 액세스할 수 있습니다.  
  
```vb  
Try  
   rs.DeleteItem("/Report1")  
  
Catch e As SoapException  
   Console.WriteLine(e.Detail("HelpLink").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.DeleteItem("/Report1");  
}  
  
catch (SoapException e)  
{  
   Console.WriteLine(e.Detail["HelpLink"].InnerXml);  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Detail 속성을 사용하여 특정 오류 처리](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
