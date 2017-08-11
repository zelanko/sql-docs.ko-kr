---
title: "웹 서비스 인증 | Microsoft Docs"
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
- Web service [Reporting Services], authentication
- XML Web service [Reporting Services], authentication
- Report Server Web service, authentication
ms.assetid: 852b4947-a090-4e54-8555-5a503945ceab
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: be7e76aa26ca4b94afd2e32b40b9fbfbe92b170d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="web-service-authentication"></a>웹 서비스 인증
  Windows 인증 또는 기본 인증을 사용하여 보고서 서버 웹 서비스에 대한 호출을 인증할 수 있습니다. 보고서 서버에 SOAP 요청을 하는 클라이언트는 지원되는 인증 프로토콜 중 하나의 클라이언트 부분을 구현해야 합니다. 사용 하는 경우는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], 인증을 구현 하는 관리 코드 HTTP 클래스를 사용할 수 있습니다. 이러한 API를 사용하면 SOAP 요청과 함께 인증 정보를 쉽게 보낼 수 있습니다.  
  
 보고서 서버 웹 서비스에 호출하기 전에 적절한 자격 증명이 없는 경우 호출이 실패합니다. 실행 시 자격 전달할 수 있습니다는 웹 서비스를 설정 하 여는 **자격 증명** 해당 메서드를 호출 하기 전에 웹 서비스를 나타내는 클라이언트 개체의 속성입니다.  
  
 다음 섹션에는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]를 사용하여 자격 증명을 보내는 예제 코드가 포함되어 있습니다.  
  
## <a name="windows-authentication"></a>Windows 인증  
 다음 코드는 Windows 자격 증명을 웹 서비스에 전달합니다.  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
ReportingService rs = new ReportingService();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
```  
  
## <a name="basic-authentication"></a>기본 인증  
 다음 코드는 기본 자격 증명을 웹 서비스에 전달합니다.  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = New System.Net.NetworkCredential("username", "password", "domain")  
```  
  
```csharp  
ReportingService service = new ReportingService();  
service.Credentials = new System.Net.NetworkCredential("username", "password", "domain");  
```  
  
 보고서 서버 웹 서비스의 메서드를 호출하기 전에 먼저 자격 증명을 설정해야 합니다. 오류 코드는 HTTP 401 오류를 수신 하는 자격 증명을 설정 하지 않은 경우: 액세스가 거부 되었습니다. 을 사용 하지만 자격 증명을 설정한 후 필요가 없습니다는 동일한 서비스 변수를 사용 하 여 계속으로 다시 설정 하기 전에 서비스를 인증 해야 합니다 (예: *rs*).  
  
## <a name="custom-authentication"></a>사용자 지정 인증  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에는 개발자가 보안 확장 프로그램이라고 하는 사용자 지정 인증 확장 프로그램을 디자인하고 개발할 수 있도록 프로그래밍 API가 포함되어 있습니다. 자세한 내용은 [Implementing a Security Extension](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
