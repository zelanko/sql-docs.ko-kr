---
title: "보고를 사용 하 여 Services SOAP 헤더 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 08aec184077b69d05939fe493bf677043beb99d3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="using-reporting-services-soap-headers"></a>Reporting Services SOAP 헤더 사용
  SOAP를 사용한 웹 서비스 메서드와의 통신은 표준 형식을 따릅니다. 이 형식의 일부는 XML 문서로 인코딩되는 데이터입니다. XML 문서는 루트 이루어져 **봉투 (envelope)** 요소에 구성 된 필수 **본문** 요소와 선택적 **헤더** 요소입니다. **본문** 요소는 메시지의 특정 데이터를 포함 합니다. 선택적 **헤더** 요소는 특정 메시지 직접적으로 관련 된 추가 정보를 포함할 수 있습니다. 각 자식 요소는 **헤더** 요소는 SOAP 헤더 라고 합니다.  
  
 SOAP 헤더가 메시지와 관련된 데이터를 포함할 수는 있지만 일반적으로 웹 서버 인프라에서 처리되는 정보를 포함합니다.  
  
 SOAP 헤더에서 사용 하기 위해 몇 가지 클래스를 정의 하는 보고서 서버 웹 서비스: <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader>, 및 <xref:ReportExecution2005.ExecutionHeader>합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[일괄 처리 방법](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|<xref:ReportService2005.BatchHeader>를 사용하여 여러 작업을 단일 트랜잭션으로 일괄 처리하는 방법을 설명합니다.|  
|[실행 상태 식별](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|세션 상태를 관리 하는 방법에 설명 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 사용 하 여 **SessionHeader**합니다.|  
|[GetProperties 메서드에 대 한 항목 Namespace를 설정](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|<xref:ReportService2010.ReportingService2010.GetProperties%2A> 메서드 및 <xref:ReportService2010.ItemNamespaceHeader> SOAP 헤더를 사용하여 항목의 경로나 ID를 기반으로 속성을 검색하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [기술 참조 &#40; Ssrs&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  

