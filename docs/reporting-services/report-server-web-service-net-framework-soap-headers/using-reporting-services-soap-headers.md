---
title: Reporting Services SOAP 헤더 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service-net-framework-soap-headers
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9c07ce717a26e4a65f40ce651608c10adeccd3cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33024840"
---
# <a name="using-reporting-services-soap-headers"></a>Reporting Services SOAP 헤더 사용
  SOAP를 사용한 웹 서비스 메서드와의 통신은 표준 형식을 따릅니다. 이 형식의 일부는 XML 문서로 인코딩되는 데이터입니다. XML 문서는 루트 **Envelope** 요소로 구성되고, 이것은 다시 필수 **Body** 요소와 선택적 **Header** 요소로 구성됩니다. **Body** 요소는 메시지 관련 데이터를 포함합니다. 선택적 **Header** 요소는 특정 메시지와 직접 관련되지 않은 추가 정보를 포함할 수 있습니다. **Header** 요소의 각 자식 요소를 SOAP 헤더라고 합니다.  
  
 SOAP 헤더가 메시지와 관련된 데이터를 포함할 수는 있지만 일반적으로 웹 서버 인프라에서 처리되는 정보를 포함합니다.  
  
 보고서 서버 웹 서비스는 SOAP 헤더에서 사용할 여러 클래스를 정의합니다. <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader> 및 <xref:ReportExecution2005.ExecutionHeader>  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[일괄 처리 메서드](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|<xref:ReportService2005.BatchHeader>를 사용하여 여러 작업을 단일 트랜잭션으로 일괄 처리하는 방법을 설명합니다.|  
|[실행 상태 식별](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|**SessionHeader**를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 세션 상태를 관리하는 방법을 설명합니다.|  
|[GetProperties 메서드에 대한 항목 네임스페이스 설정](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|<xref:ReportService2010.ReportingService2010.GetProperties%2A> 메서드 및 <xref:ReportService2010.ItemNamespaceHeader> SOAP 헤더를 사용하여 항목의 경로나 ID를 기반으로 속성을 검색하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [기술 참조&#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
