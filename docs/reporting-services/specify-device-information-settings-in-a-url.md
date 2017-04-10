---
title: "URL에 장치 정보 설정 지정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "장치 정보 설정 [Reporting Services], URL"
  - "URL 액세스 [Reporting Services], 장치 정보 설정"
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# URL에 장치 정보 설정 지정
  장치 정보 설정은 렌더링 확장 프로그램에 전달되는 매개 변수입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 보고서 서버 웹 서비스의 메서드를 사용하여 보고서를 렌더링하는 경우 **DeviceInfo** XML 요소가 입력 매개 변수로 전달됩니다. **DeviceInfo** 요소의 자식 요소는 다양한 렌더링 확장 프로그램의 장치 정보 설정마다 다릅니다. *rc:tag=value* 매개 변수 문자열을 사용하여 URL에 장치 정보 설정을 포함시킬 수 있습니다. 여기서 *tag*는 액세스되는 장치 정보 설정 요소의 이름입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 장치 정보 설정에 대한 자세한 내용은 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)을 참조하세요.  
  
## 예제  
 다음 예에서는 이미지 렌더링 확장 프로그램의 *OutputFormat* 장치 정보 설정을 사용하여 지정된 보고서의 형식을 JPEG으로 설정합니다(읽기 쉽도록 줄 바꿈 추가됨).  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## 관련 항목:  
 [URL 액세스&#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](../reporting-services/url-access-parameter-reference.md)  
  
  