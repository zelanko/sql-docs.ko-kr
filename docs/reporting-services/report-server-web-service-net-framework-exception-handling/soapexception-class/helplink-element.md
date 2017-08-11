---
title: "HelpLink 요소 | Microsoft Docs"
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
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 683da36a3015ee177935823d234968c8486eb51c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="helplink-element"></a>HelpLink 요소
  **HelpLink** 의 요소는 **세부** 속성은 보고서 서버에 의해 생성 되는 URL 문자열입니다. 이 URL은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 도움말 및 지원에서 관리되는 웹 페이지를 대상으로 하며 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 발생하는 특정 오류에 대한 추가 도움말 및 기술 자료 문서를 제공합니다. URL의 구문은 다음과 같습니다.  
  
 **http://**www.microsoft.com**/**products**/**ee**/**transform.aspx**? EvtSrc**=v*alue***&EvtID**=*value***&ProdName**=*value***&ProdVer**=*value*  
  
 다음 표에서의 인수는 **HelpLink** URL입니다.  
  
|인수|Value|  
|--------------|-----------|  
|**EvtSrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**EvtID**|보고서 서버 오류 코드입니다(예: rsReservedItem).|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services". 제품 이름 값은 URL로 인코딩됩니다.|  
|**제품 버전**|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 버전 번호입니다. "8.00"은 값 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]합니다.|  
  
 다음 예제는 **HelpLink** 오류 코드에 대해 반환 되는 URL **rsReservedItem**합니다. 이 오류는 사용자가 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 예약된 항목을 수정하거나 삭제하려고 시도할 때 발생합니다.  
  
```  
http://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 에 액세스할 수 있습니다는 **HelpLink** 사용 하 여 코드의 요소는 **SoapException** 클래스입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Detail 속성을 사용 하 여 특정 오류 처리](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
