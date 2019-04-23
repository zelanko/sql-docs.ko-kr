---
title: 웹 서비스 메서드 호출 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 87f1485b4e3c0ed064e42bb3b411fece96eba8d2
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158469"
---
# <a name="calling-web-service-methods"></a>웹 서비스 메서드 호출
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 프록시 클래스를 사용하여 웹 서비스 작업을 호출할 경우 해당 클래스의 메서드를 사용합니다. 이러한 메서드는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 클래스 라이브러리의 다른 클래스 메서드와 같이 응답합니다. 모든 웹 서비스 메서드는 공용 액세스 권한을 가지며 알맞은 수의 인수와 인수 유형을 제공하도록 요구합니다. 프로젝트에서 프록시 클래스의 인스턴스를 만들었으면 메서드를 호출하여 보고서 서버를 통해 보고 작업을 수행할 수 있습니다. 다음 C# 코드는 <xref:ReportService2010.ReportingService2010> 프록시 클래스의 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 메서드 사용을 보여 줍니다. 이 코드는 보고서 서버 데이터베이스의 모든 항목 목록이 포함된 <xref:ReportService2010.CatalogItem> 개체 배열을 반환하는 웹 서비스 재귀 호출을 수행하는 데 사용됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../report-server-web-service.md)   
 [기술 참조&#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
