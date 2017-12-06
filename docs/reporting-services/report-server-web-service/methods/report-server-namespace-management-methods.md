---
title: "보고서 서버 네임스페이스 관리 메서드 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- reports [Reporting Services], managing
- management methods [Reporting Services]
- methods [Reporting Services], about methods
- methods [Reporting Services]
ms.assetid: 2aa43ce9-f51e-408a-8ce0-b40d3dd62561
caps.latest.revision: "37"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 80c4c1221b104986f1362d38db37fb71fe2f2ba6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="report-server-namespace-management-methods"></a>보고서 서버 네임스페이스 관리 메서드
  보고서 서버 관리 웹 서비스에는 보고서 서버 데이터베이스에서 보고서, 폴더 및 리소스를 관리하는 데 사용할 수 있는 메서드가 포함됩니다.  
  
|메서드|동작|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CancelJob%2A>|작업 실행을 취소합니다.|  
|<xref:ReportService2010.ReportingService2010.CreateFolder%2A>|보고서 서버 데이터베이스 또는 SharePoint 라이브러리에 폴더를 추가합니다.|  
|<xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A>|보고서 서버 데이터베이스 또는 SharePoint 라이브러리에 새 항목을 추가합니다. 이 메서드는 **보고서**, **모델**, **데이터 집합**, **구성 요소**, **리소스** 및 **DataSource** 항목 종류에 적용됩니다.|  
|M:ReportService2010.ReportingService2010.CreateReportEditSession(System.String,System.String,System.Byte[],ReportService2010.Warning[]@)|새 보고서 편집 세션을 만듭니다.|  
|<xref:ReportService2010.ReportingService2010.DeleteItem%2A>|보고서 서버 데이터베이스 또는 SharePoint 라이브러리에서 항목을 제거합니다.|  
|<xref:ReportService2010.ReportingService2010.FindItems%2A>|보고서 서버 데이터베이스 또는 SharePoint 라이브러리에서 지정된 검색 조건과 일치하는 항목을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.FireEvent%2A>|제공된 매개 변수를 기준으로 이벤트를 트리거합니다.|  
|<xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>|지정된 확장 프로그램에 대한 설정 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.GetItemType%2A>|항목이 존재하는 경우 보고서 서버 데이터베이스 또는 SharePoint 라이브러리에서 항목의 유형을 검색합니다.|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|보고서 서버 데이터베이스 또는 SharePoint 라이브러리의 항목에 대한 하나 이상의 속성 값을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>|항목의 정의 또는 콘텐츠를 검색합니다. 이 메서드는 **보고서**, **모델**, **데이터 집합**, **구성 요소**, **리소스** 및 **DataSource** 항목 종류에 적용됩니다.|  
|<xref:ReportService2010.ReportingService2010.GetItemReferences%2A>|항목과 연결된 카탈로그 항목 참조 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.GetReportServerConfigInfo%2A>|스케일 아웃 배포에 있는 모든 보고서 서버 인스턴스 또는 연결된 보고서 서버 인스턴스에 대한 정보를 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|시스템 속성을 하나 이상 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListChildren%2A>|지정된 폴더의 자식 목록을 가져옵니다.|  
|<xref:ReportService2010.ReportingService2010.ListDatabaseCredentialRetrievalOptions%2A>|지원되는 자격 증명 검색 옵션 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListEvents%2A>|보고서 서버 구성 파일에 나타나는 이벤트 확장 프로그램 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListJobs%2A>|보고서 서버에서 실행 중인 작업 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListExtensions%2A>|지정된 확장 유형에 대해 구성된 확장 프로그램 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListExtensionTypes%2A>|지원되는 확장 유형 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListItemTypes%2A>|지원되는 카탈로그 항목 유형 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListJobActions%2A>|지원되는 작업 동작 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListJobStates%2A>|지원되는 작업 상태 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListJobTypes%2A>|지원되는 작업 유형 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListParents%2A>|지정된 항목의 부모 항목을 검색합니다.|  
|<xref:ReportService2010.ReportingService2010.ListSecurityScopes%2A>|지원되는 보안 범위 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.Logoff%2A>|웹 서비스 요청을 하는 현재 사용자를 로그아웃시킵니다. 이 메서드는 기본 모드에만 적용됩니다.|  
|<xref:ReportService2010.ReportingService2010.LogonUser%2A>|보고서 서버 웹 서비스에 사용자를 로그온하고 사용자 요청을 인증합니다. 이 메서드는 기본 모드에만 적용됩니다.|  
|<xref:ReportService2010.ReportingService2010.SetItemReferences%2A>|항목과 연결된 카탈로그 항목을 설정합니다.|  
|<xref:ReportService2010.ReportingService2010.MoveItem%2A>|항목을 이동하거나 항목 이름을 바꿉니다.|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|항목 속성을 하나 이상 설정합니다.|  
|<xref:ReportService2010.ReportingService2010.SetItemDefinition%2A>|지정된 항목의 정의 또는 콘텐츠를 설정합니다. 이 메서드는 **보고서**, **모델**, **데이터 집합**, **구성 요소**, **리소스** 및 **DataSource** 항목 종류에 적용됩니다.|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|보고서 서버 또는 SharePoint 팜에서 시스템 속성을 하나 이상 설정합니다.|  
|<xref:ReportService2010.ReportingService2010.ValidateExtensionSettings%2A>|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 확장 프로그램 설정의 유효성을 검사합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [보고서 서버 웹 서비스 메서드](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [기술 참조&#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
