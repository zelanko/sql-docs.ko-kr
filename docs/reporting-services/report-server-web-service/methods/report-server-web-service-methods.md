---
title: 보고서 서버 웹 서비스 메서드 | Microsoft Docs
description: 보고서 서버 웹 서비스에는 생성된 클래스를 사용하여 공개된 웹 서비스 엔드포인트를 통해 제공되는 구성 요소 기능에 따른 메서드가 포함되어 있습니다.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 88a79f66c6cb062dfe563883fbc5fef5eeebfe08
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79198360"
---
# <a name="report-server-web-service-methods"></a>보고서 서버 웹 서비스 메서드
  보고서 서버 웹 서비스에는 구성 요소 기능에 따라 여러 범주의 메서드가 있습니다. 이러한 메서드는 <xref:ReportService2010.ReportingService2010> 및 <xref:ReportExecution2005.ReportExecutionService> 클래스의 멤버로 노출되는 여러 개의 웹 서비스 엔드포인트(세 개는 보고서 관리용, 하나는 보고서 실행용)를 통해 제공됩니다. 이러한 클래스는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK에 포함된 wsdl.exe와 같은 프록시 클래스 도구를 통해 생성될 수 있습니다. 보고서 서버 웹 서비스 및 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]에 대한 자세한 내용은 [웹 서비스와 .NET Framework를 사용하여 애플리케이션 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)를 참조하세요.  
  
## <a name="endpoints-and-methods"></a>엔드포인트 및 메서드  
 다음 표는 보고서 서버 웹 서비스의 엔드포인트와 <xref:ReportService2010.ReportingService2010> 엔드포인트에서 제공하는 메서드의 범주를 나열합니다. 다른 엔드포인트에서 사용할 수 있는 메서드에 대한 자세한 내용은 [기술 참조&#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)를 참조하세요.  
  
|항목|Description|  
|-----------|-----------------|  
|[보고서 서버 웹 서비스 엔드포인트](../../../reporting-services/report-server-web-service/methods/report-server-web-service-endpoints.md)|보고서 서버 웹 서비스의 관리 및 실행 엔드포인트를 설명합니다.|  
|[보고서 서버 네임스페이스 관리 메서드](../../../reporting-services/report-server-web-service/methods/report-server-namespace-management-methods.md)|보고서 서버 데이터베이스를 관리하는 데 사용할 수 있는 메서드를 설명합니다. 특히 폴더 및 리소스를 관리하고 항목 속성을 설정할 수 있습니다.|  
|[권한 부여 메서드](../../../reporting-services/report-server-web-service/methods/authorization-methods.md)|태스크, 역할 및 정책을 관리하는 데 사용할 수 있는 메서드를 설명합니다.|  
|[데이터 원본 및 연결 메서드](../../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md)|보고서에 대한 데이터 원본 연결과 자격 증명 정보를 설정하고 관리하는 데 사용할 수 있는 메서드를 설명합니다.|  
|[보고서 매개 변수 메서드](../../../reporting-services/report-server-web-service/methods/report-parameters-methods.md)|보고서의 매개 변수를 설정하고 검색하는 데 사용할 수 있는 메서드를 설명합니다.|  
|[모델 메서드 - 보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/methods/model-methods-report-server-web-service.md)|모델을 관리하는 데 사용할 수 있는 메서드를 설명합니다.|  
|[렌더링 및 실행 메서드](../../../reporting-services/report-server-web-service/methods/rendering-and-execution-methods.md)|보고서 실행, 렌더링 및 캐싱을 관리하는 데 사용할 수 있는 메서드를 설명합니다.|  
|[보고서 기록 메서드](../../../reporting-services/report-server-web-service/methods/report-history-methods.md)|보고서 기록 스냅샷을 만들고 관리하는 데 사용할 수 있는 메서드를 설명합니다.|  
|[일정 예약 메서드](../../../reporting-services/report-server-web-service/methods/scheduling-methods.md)|보고서 서버에서 사용되는 공유 일정 및 캐시 새로 고침 계획을 만들고 관리하는 데 사용할 수 있는 메서드를 설명합니다.|  
|[구독 및 배달 메서드](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)|구독 및 보고서 배달을 만들고 관리하는 데 사용할 수 있는 메서드를 설명합니다.|  
|[링크된 보고서 메서드](../../../reporting-services/report-server-web-service/methods/linked-reports-methods.md)|링크된 보고서를 만들고 관리하는 데 사용할 수 있는 메서드를 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SOAP API 액세스](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)   
 [웹 서비스와 .NET Framework를 사용하여 애플리케이션 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [기술 참조&#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
