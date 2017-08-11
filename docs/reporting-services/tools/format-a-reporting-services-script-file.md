---
title: "Reporting Services 스크립트 파일 형식 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [Reporting Services], formats
- formats [Reporting Services], script files
ms.assetid: 85a207dd-4e0f-4d40-a41e-0c75f65d719c
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de06ca0018df176e84db7e16e38c3c2021811fda
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="format-a-reporting-services-script-file"></a>Reporting Services 스크립트 파일 형식 지정
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 스크립트는 WSDL(Web Service Description Language)을 기반으로 하는 프록시에 대해 작성된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 코드 파일로, Reporting Services SOAP API를 정의합니다. 스크립트 파일은 확장명이 .rss인 유니코드 또는 UTF-8 텍스트 파일로 저장됩니다.  
  
 이 스크립트 파일은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 모듈로 사용되며 사용자 정의 프로시저 및 모듈 수준 변수를 포함할 수 있습니다. 스크립트 파일이 성공적으로 실행되려면 Main 프로시저를 포함해야 합니다. Main 프로시저는 스크립트 파일이 실행될 때 액세스되는 첫 번째 프로시저입니다. Main은 웹 서비스 작업을 추가하고 사용자 정의 하위 프로시저를 실행할 수 있는 위치입니다. 다음 코드에서는 Main 프로시저를 만듭니다.  
  
```  
Public Sub Main()  
    ' Your code goes here.  
End Sub  
```  
  
 스크립트 환경에서는 자동으로 보고서 서버에 연결하고, 웹 프록시 클래스를 만들고, 웹 서비스 프록시 개체에 대한 참조 변수(*rs*)를 생성합니다. 직접 만드는 개별 문은 웹 서비스 라이브러리에서 사용할 수 있는 웹 서비스 작업 중 원하는 작업을 수행하기 위해 *rs* 모듈 수준 변수만 참조하면 됩니다. 다음 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 코드는 스크립트 파일 내에서 웹 서비스 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 메서드를 호출합니다.  
  
```  
Public Sub Main()  
    Dim items() As CatalogItem  
    items = rs.ListChildren("/", True)  
  
    Dim item As CatalogItem  
    For Each item In items  
        Console.WriteLine(item.Name)  
    Next item  
End Sub   
```  
  
> [!IMPORTANT]  
>  사용자 자격 증명은 스크립트 환경에서 관리되며 RS.exe를 사용하여 명령 프롬프트 인수를 통해 전달됩니다. *rs* 변수를 사용하여 웹 서비스의 인증을 설정할 수도 있지만 스크립트 환경을 사용하는 것이 좋습니다. 스크립트 파일 자체에서 웹 서비스를 인증하지 않아도 됩니다. 스크립트 환경 인증에 대한 자세한 내용은 [RS.exe 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)를 참조하세요.  
  
 스크립트 파일 내에서는 네임스페이스를 선언하지 않습니다. 스크립팅 환경에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] namespaces available to you: **System.Web.Services**, **System.Web.Services.Protocols**, **System.Xml**, and **System.IO**.  
  
 스크립트 예제는 [SQL Server Reporting Services 제품 예제(SQL Server Reporting Services Product Samples)](http://go.microsoft.com/fwlink/?LinkId=177889)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 서버 웹 서비스](../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [기술 참조 &#40; Ssrs&#41;](../../reporting-services/technical-reference-ssrs.md)   
 [RS.exe 유틸리티 &#40; Ssrs&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)  
  
  
