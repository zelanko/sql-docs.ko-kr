---
title: Reporting Services 모바일 보고서에 대한 데이터 준비 | Microsoft Docs
ms.custom: ''
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8adce9ad-6a08-4d20-b1cf-d3c45544d8de
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 731b28c5f2f269d9527a7ba846beec747680ffe5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-data-for-reporting-services-mobile-reports"></a>Prepare data for Reporting Services mobile reports
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] 에서는 필터링, 집계 및 시간 조각과 같은 다양하고 복잡한 데이터 작업을 지원합니다. 이 문서에서는 데이터를 준비하는 동안 유념할 몇 가지 사항을 제공합니다. 데이터 사전 집계로 모바일 보고서 만들기 및 사용을 모두 최적화할 수 있으며 일부 모바일 보고서 디자인에서 이를 필요로 합니다.   
  
## <a name="date-and-time-formats"></a>날짜 및 시간 형식 
모바일 보고서에서 사용할 날짜 및 시간 간격을 처리할 때 특히 TimeNavigator로 작업할 때 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 에서 이를 식별할 수 있도록 날짜/시간 열 형식을 제대로 지정하는 것이 중요합니다. 다음은 유효한 날짜/시간 형식의 예입니다.  
  
    05/01/2009    
    2009-05-01    
    05/01/2009 14:57:32.8    
    2009-05-01 14:57:32.8    
    2009-05-01T14:57:32.8375298-04:00    
    5/01/2008 14:57:32.80 -07:00    
    1 May 2008 2:57:32.8 PM    
    Fri, 15 May 2009 20:10:57 GMT    
  
대부분의 경우 날짜 및 시간 기반 데이터 집합이 하나 이상의 날짜/시간 간격(예: 시간별, 일별, 월별, 분기별 및 연간)으로 설명됩니다. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 에서는 다양한 세분성의 여러 테이블을 조합하고 이를 단일 모바일 보고서에 표시할 수 있습니다. 그러나 최종 모바일 보고서에 사용자에게 표시할 날짜/시간 필터 옵션을 결정할 때 도움이 될 수 있도록 원래 데이터 집합에서 관련 간격을 염두에 두어야 합니다.  

[!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 다차원 및 테이블 형식 모델의 날짜 필드는 공유 데이터 집합에서 날짜 서식이 손실될 수 있습니다. 서식을 유지하는 솔루션은 [모바일 보고서에서 Analysis Services에 대한 날짜 형식 지정 유지](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) 를 참조하세요.
  
## <a name="preparing-filter-data"></a>필터 데이터 준비 ##  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 에서 날짜/시간 필드 및 키 필드 모두를 기반으로 데이터를 필터링할 수 있습니다. 키 필드는 숫자일 수 있지만 대부분의 경우 ID 또는 문자열 값입니다. 선택 목록 등 탐색기 요소와 함께 사용할 필터 필드를 준비하려면 필터 키가 데이터 테이블에서 단일 열이어야 합니다. 이런 방식으로 필터 열의 값에 따라 테이블 행을 그룹화할 수 있습니다. 서로 다른 필터 키 또는 필터 조건을 포함하는 여러 열에 대해 모바일 보고서에서 여러 필터 탐색기를 계층적 또는 개별적으로 함께 사용할 수 있습니다.  
  
| 산업  | Country   | Region    |  
| ------------- | ------------- | ------------- |  
| 은행     | 아프가니스탄   | 아시아      |  
| 상용 및 전문 서비스 | 아프가니스탄 | 아시아 |  
| 식품, 주류 및 담배 | 아프가니스탄 | 아시아 |  
| 미디어 | 아프가니스탄 | 아시아 |  
| 제약 | 아프가니스탄 | 아시아 |  
| 식품 및 주요 식품 소매 | 알바니아 | 유럽 |  
  
  
키 기반 필터는 트리 구조에서 선택 목록과 함께 사용하기 위해 계층적으로 구조화할 수도 있습니다. 이러한 종류의 시나리오에서 사용할 데이터를 준비하려면 계층 구조를 설명하는 조회 테이블을 만듭니다. 전체 계층 구조에서 노드가 속하는 위치를 나타내는 데 키 열 및 부모 키 열을 포함하는 테이블 구조를 사용합니다.  
  
이 테이블에서 ParentKey 항목은 ItemKey 열에 먼저 나열된 후 해당 자식 항목 옆에 ParentItemKey 열에 나열됩니다.   
  
|ItemKey    | ParentItemKey |  
| ------------- | ------------- |  
| 금융    |   |  
| 산업   |   |  
| 소비재 |    |  
| 자유재량 소비재 |  |     
| 의료   |   |  
| 정보 기술 |  |  
| 은행 | 금융 |  
| 부동산 | 금융 |  
| 분산 금융 |  금융 |   
| 보험 |   금융 |  
| 상용 및 전문 서비스 |  산업 |  
| 자본재 |   산업 |  
| 운송 |  산업 |  
| 식품, 주류 및 담배 |    소비재 |  
| 식품 및 주요 식품 소매 |    소비재 |  
| 가정 및 개인 제품 | 소비재 |  
| 미디어 | 자유재량 소비재 |  
| 자동차 및 부품 |  자유재량 소비재 |  
| 내구 소비재 및 의류 |자유재량 소비재 |  
| 고객 서비스 |   자유재량 소비재 |  
| 소매 | 자유재량 소비재 |  
| 제약   | 의료 |  
| 의료 장비 및 서비스 |    의료 |  
| 소프트웨어 및 서비스 | 정보 기술 |  
| 기술 하드웨어 및 장비   | 정보 기술 |  
| 원격 통신 서비스 |정보 기술 |  
  
### <a name="see-also"></a>관련 항목:  
- [Reporting Services 모바일 보고서에 대한 Excel 데이터 준비](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)  
- [모바일 보고서에서 Analysis Services에 대한 날짜 형식 지정 유지](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md)
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
  
  

