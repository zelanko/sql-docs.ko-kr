---
title: "데이터 원본 및 연결 메서드 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- data sources [Reporting Services], methods
ms.assetid: 50999b52-fc7c-4333-9fb0-d04c37a4c90f
caps.latest.revision: "38"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8eba13519bae937a6f22873adbe3386a4e6fc379
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="data-sources-and-connection-methods"></a>데이터 원본 및 연결 메서드
  이러한 메서드를 사용하여 데이터 원본 연결 및 자격 증명을 설정하고 관리할 수 있습니다.  
  
|메서드|작업|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateDataSource%2A>|보고서 서버 데이터베이스 또는 SharePoint 라이브러리에서 새 데이터 원본을 만듭니다.|  
|<xref:ReportService2010.ReportingService2010.DisableDataSource%2A>|사용하도록 설정된 데이터 원본을 사용하지 않도록 설정합니다.|  
|<xref:ReportService2010.ReportingService2010.EnableDataSource%2A>|사용하지 않도록 설정된 데이터 원본을 사용하도록 설정합니다.|  
|<xref:ReportService2010.ReportingService2010.GetDataSourceContents%2A>|데이터 원본의 내용을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.GetItemDataSourcePrompts%2A>|지정된 항목의 데이터 원본 프롬프트를 가져옵니다.|  
|<xref:ReportService2010.ReportingService2010.GetItemDataSources%2A>|카탈로그에 있는 항목의 데이터 원본을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListDependentItems%2A>|지정된 카탈로그 항목을 참조하는 카탈로그 항목 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.ListSubscriptionsUsingDataSource%2A>|지정된 데이터 원본과 연결된 구독 목록을 반환합니다.|  
|<xref:ReportService2010.ReportingService2010.SetDataSourceContents%2A>|데이터 원본과 연결된 연결 속성을 설정합니다.|  
|<xref:ReportService2010.ReportingService2010.SetItemDataSources%2A>|보고서 서버 데이터베이스 또는 SharePoint 라이브러리에 있는 항목의 데이터 원본을 설정합니다.|  
|<xref:ReportService2010.ReportingService2010.TestConnectForDataSourceDefinition%2A>|데이터 원본에 대한 연결을 테스트합니다. 이 메서드는 데이터 원본의 직접 테스트를 지원합니다.|  
|<xref:ReportService2010.ReportingService2010.TestConnectForItemDataSource%2A>|데이터 원본에 대한 연결을 테스트합니다. 이 메서드는 보고서나 모델 및 공유 데이터 원본에서 사용하는 게시된 데이터 원본의 테스트를 지원합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [보고서 서버 웹 서비스 메서드](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [기술 참조&#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
