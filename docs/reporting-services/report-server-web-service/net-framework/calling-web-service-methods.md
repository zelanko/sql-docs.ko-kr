---
title: "웹 서비스 메서드를 호출 합니다. | Microsoft Docs"
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
- Web service [Reporting Services], SOAP
- Web service [Reporting Services], calls
- calling Web service
- Report Server Web service, SOAP
- XML Web service [Reporting Services], calls
- Report Server Web service, calls
- XML Web service [Reporting Services], SOAP
- SOAP [Reporting Services], calls
ms.assetid: f6f0c6e3-8bb5-4c44-9d19-1872edc72746
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 31966275516c514ebfc8809090a0342be70f1d53
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="calling-web-service-methods"></a>웹 서비스 메서드 호출
  사용 하는 경우는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 프록시 클래스를 웹 서비스 작업 호출 해당 클래스의 메서드를 사용 하 여 그렇게 합니다. 이러한 메서드는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 클래스 라이브러리의 다른 클래스 메서드와 같이 응답합니다. 모든 웹 서비스 메서드는 공용 액세스 권한을 가지며 알맞은 수의 인수와 인수 유형을 제공하도록 요구합니다. 프로젝트에서 프록시 클래스의 인스턴스를 만들었으면 메서드를 호출하여 보고서 서버를 통해 보고 작업을 수행할 수 있습니다. 다음 C# 코드에서는 사용 된 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 의 메서드는 <xref:ReportService2010.ReportingService2010> 프록시 클래스입니다. 이 코드는 보고서 서버 데이터베이스의 모든 항목 목록이 포함된 <xref:ReportService2010.CatalogItem> 개체 배열을 반환하는 웹 서비스 재귀 호출을 수행하는 데 사용됩니다.  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
Dim items As CatalogItem() = rs.ListChildren("/", True)  
```  
  
```csharp  
ReportingService2010 rs = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
CatalogItem[] items = rs.ListChildren("/", true);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [기술 참조 &#40; Ssrs&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

