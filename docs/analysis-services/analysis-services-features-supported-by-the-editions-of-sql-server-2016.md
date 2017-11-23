---
title: "Analysis Services의 SQL Server 2016 버전에서 지 원하는 기능 | Microsoft Docs"
ms.custom: 
ms.date: 06/29/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: "4"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 05804908eb3d5b4d519516519eb091e92aeaee34
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="analysis-services-features-supported-by-the-editions-of-sql-server-2016"></a>SQL Server 2016 버전에서 지원하는 Analysis Services 기능
[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

이 항목에서는 SQL Server 2016 Analysis Services의 다양 한 버전에서 지 원하는 기능에 대 한 세부 정보를 제공 합니다. Evaluation 및 Developer 버전에서 지 원하는 기능, Enterprise edition을 참조 하십시오.

## <a name="analysis-services-servers"></a>Analysis Services (서버)
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|확장 가능 공유 데이터베이스|예||||||예|  
|데이터베이스 백업/복원 및 연결/분리|예|예|||||예|  
|데이터베이스 동기화|예||||||예|  
|Always On 장애 조치(failover) 클러스터 인스턴스|예<br /><br /> 운영 체제가 지원하는 최대 크기의 노드 수|예<br /><br /> 노드 2개 지원|||||예<br /><br /> 운영 체제가 지원하는 최대 크기의 노드 수|  
|프로그래밍 기능(AMO, ADOMD.Net, OLEDB, XML/A, ASSL, TMSL)|예|예|||||예|  
  
## <a name="tabular-models"></a>테이블 형식 모델 
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|계층 구조|예|예|||||예|  
|KPI|예|예|||||예|  
|큐브 뷰|예||||||예|  
|번역|예|예|||||예|  
|DAX 계산, DAX 쿼리, MDX 쿼리|예|예|||||예|  
|행 수준 보안|예|예|||||예|  
|여러 파티션|예||||||예|  
|메모리 내 저장소 모드|예|예|||||예|  
|DirectQuery 저장소 모드|예||||||예|  

## <a name="multidimensional-models"></a>다차원 모델 
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|반가산적 측정값|예|아니오 <sup>1</sup>|||||예|  
|계층 구조|예|예|||||예|  
|KPI|예|예|||||예|  
|큐브 뷰|예||||||예|  
|작업|예|예|||||예|  
|계정 인텔리전스|예|예|||||예|  
|시간 인텔리전스|예|예|||||예|  
|사용자 지정 롤업|예|예|||||예|  
|큐브 쓰기 저장(writeback)|예|예|||||예|  
|차원 쓰기 저장(Writeback)|예||||||예|  
|셀 쓰기 저장(writeback)|예|예|||||예|  
|드릴스루|예|예|||||예|  
|고급 계층 유형(부모-자식 및 비정형 계층 구조)|예|예|||||예|  
|고급 차원(참조 차원, 다 대 다 차원)|예|예|||||예|  
|연결된 측정값 및 차원|예|예  <sup>2</sup> |||||예|  
|번역|예|예|||||예|  
|Aggregations|예|예|||||예|  
|여러 파티션|예|예, 최대 3|||||예|  
|자동 관리 캐싱|예||||||예|  
|사용자 지정 어셈블리(저장 프로시저)|예|예|||||예|  
|MDX 쿼리 및 스크립트|예|예|||||예|  
|DAX 쿼리|예|예|||||예|  
|역할 기반 보안 모델|예|예|||||예|  
|차원 및 셀 수준 보안|예|예|||||예|  
|확장 가능 문자열 저장소|예|예|||||예|  
|MOLAP, ROLAP 및 HOLAP 저장소 모델|예|예|||||예|  
|이진 및 압축 XML 전송|예|예|||||예|  
|밀어넣기 모드 처리|예||||||예|  
|직접 쓰기 저장|예||||||예|  
|측정값 식|예||||||예|  
  
 <sup>1</sup> Standard Edition에서 LastChild 반가산적 측정값은 지원되지만 None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren 및 ByAccount와 같은 다른 반가산적 측정값은 지원되지 않습니다. Sum, Count, Min, Max와 같은 가산적 측정값과 비가산적 측정값(DistinctCount)은 모든 버전에서 지원됩니다.  
  <sup>2</sup> standard edition에서는 측정값 및 차원은 동일한 데이터베이스 내에 있지만 다른 데이터베이스 또는 인스턴스에에서 아니라 연결을 지원 합니다.
  
## <a name="power-pivot-for-sharepoint"></a>SharePoint용 PowerPivot  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|공유 서비스 아키텍처를 기반으로 하는 SharePoint 팜 통합|예||||||예|  
|사용 보고|예||||||예|  
|상태 모니터링 규칙|예||||||예|  
|파워 피벗 갤러리|예||||||예|  
|파워 피벗 데이터 새로 고침|예||||||예|  
|파워 피벗 데이터 피드|예||||||예|  
  
## <a name="data-mining"></a>데이터 마이닝  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|표준 알고리즘|예|예|||||예|  
|데이터 마이닝 도구(마법사, 편집기, 쿼리 작성기)|예|예|||||예|  
|교차 유효성 검사|예||||||예|  
|마이닝 구조 데이터의 필터링된 하위 집합에 대한 모델|예||||||예|  
|시계열: ARTXP 및 ARIMA 방식 간의 사용자 지정 혼합|예||||||예|  
|시계열: 새 데이터를 사용한 예측|예||||||예|  
|무제한 동시 DM 쿼리|예||||||예|  
|데이터 마이닝 알고리즘용 고급 구성 및 튜닝 옵션|예||||||예|  
|플러그 인 알고리즘 지원|예||||||예|  
|병렬 모델 처리|예||||||예|  
|시계열: 계열 간 예측|예||||||예|  
|연결 규칙에 대한 무제한 특성|예||||||예|  
|시퀀스 예측|예||||||예|  
|naïve Bayes, 신경망, 로지스틱 회귀 분석을 위한 다중 예측 대상|예||||||예|  
  
 ## <a name="see-also"></a>관련 항목:  
 [SQL Server 2016 제품 사양](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [SQL Server 2016 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)  


