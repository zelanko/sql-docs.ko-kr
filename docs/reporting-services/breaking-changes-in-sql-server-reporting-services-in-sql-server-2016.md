---
title: "SQL Server 2016에서 SQL Server Reporting Services의 주요 변경 내용 | Microsoft Docs"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Me.Value 참조"
  - "Reporting Services, 이전 버전과의 호환성"
  - "주요 변경 내용 [Reporting Services]"
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 116
---
# SQL Server 2016에서 SQL Server Reporting Services의 주요 변경 내용
  이 항목에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 주요 변경 내용에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 응용 프로그램, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때나 사용자 지정 스크립트 또는 보고서에서 발생할 수 있습니다.  
  
  ## 보안 확장 프로그램
  
  새 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]에서 작동하도록 사용자 지정 보안 확장 프로그램을 약간 수정해야 합니다. 보안 확장 프로그램에서는 IAuthenticationExtension2 인터페이스를 사용해야 합니다.
  
  ## WMI 공급자
  
  [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 응용 프로그램 이름이 "ReportManager"에서 "ReportServerWebApp"으로 변경됩니다.
  
## 관련 항목:  
 [SQL Server 2016에서 SQL Server Reporting Services의 동작 변경 내용](http://msdn.microsoft.com/ko-kr/2a767f0f-84f2-4099-8784-1e37790f858e)   
 [Reporting Services&#40;SSRS&#41;의 새로운 기능](../Topic/What's%20New%20in%20Reporting%20Services%20\(SSRS\).md)   
 [SQL Server 2016의 SQL Server Reporting Services에서 사용되지 않는 기능](http://msdn.microsoft.com/ko-kr/3876c01e-f81d-4cce-9104-5106a8c369e6)   
 [SQL Server 2016의 SQL Server Reporting Services에서 중단된 기능](http://msdn.microsoft.com/ko-kr/d529cc96-3483-480b-9bfc-bd28b1d0ef52)  
  
  