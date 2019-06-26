---
title: Analysis Services의 SQL Server 버전에서 지 원하는 기능 | Microsoft Docs
ms.date: 06/25/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9947b10e01864f66bf26d6599e43814ab37dadc6
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388214"
---
# <a name="analysis-services-features-supported-by-sql-server-edition"></a>SQL Server 버전에서 지 원하는 analysis Services 기능
[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

이 문서에서는 다양 한 버전의 SQL Server 2016, 2017 년 2019 Analysis Services에서 지 원하는 기능을 설명 합니다. 평가판은 Enterprise edition 기능을 지원합니다.

## <a name="analysis-services-servers"></a>Analysis Services (서버)
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|확장 가능 공유 데이터베이스|예||||||예|  
|데이터베이스 백업/복원 및 연결/분리|예|예|||||사용자 계정 컨트롤|  
|데이터베이스 동기화|사용자 계정 컨트롤||||||예|  
|Always On 장애 조치(failover) 클러스터 인스턴스|예<br /><br /> 운영 체제가 지원하는 최대 크기의 노드 수|예<br /><br /> 노드 2개 지원|||||예<br /><br /> 운영 체제가 지원하는 최대 크기의 노드 수|  
|프로그래밍 기능(AMO, ADOMD.Net, OLEDB, XML/A, ASSL, TMSL)|예|예|||||예|  
  
## <a name="tabular-models"></a>테이블 형식 모델 
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|계층 구조|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|KPI|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|큐브 뷰|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|Translations|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|DAX 계산, DAX 쿼리, MDX 쿼리|사용자 계정 컨트롤|예|||||예|  
|행 수준 보안|예|예|||||예|  
|여러 파티션|예||||||사용자 계정 컨트롤|  
|계산 그룹|예 (SQL Server 2019부터)|예 (SQL Server 2019부터)|||||예 (SQL Server 2019부터)|  
|메모리 내 스토리지 모드|예|예|||||사용자 계정 컨트롤|  
|DirectQuery 모드|사용자 계정 컨트롤|예 (SQL Server 2019부터)|||||사용자 계정 컨트롤|  

## <a name="multidimensional-models"></a>다차원 모델 
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|반가산적 측정값|예|아니오 <sup>1</sup>|||||예|  
|계층|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|KPI|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|큐브 뷰|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|동작|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|계정 인텔리전스|사용자 계정 컨트롤|예|||||예|  
|시간 인텔리전스|예|예|||||사용자 계정 컨트롤|  
|사용자 지정 롤업|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|큐브 쓰기 저장(writeback)|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|차원 쓰기 저장(Writeback)|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|셀 쓰기 저장(writeback)|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|드릴스루|사용자 계정 컨트롤|예|||||예|  
|고급 계층 유형(부모-자식 및 비정형 계층 구조)|예|예|||||예|  
|고급 차원(참조 차원, 다 대 다 차원)|예|예|||||사용자 계정 컨트롤|  
|연결된 측정값 및 차원|예|예  <sup>2</sup> |||||예|  
|Translations|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|Aggregations|사용자 계정 컨트롤|예|||||예|  
|여러 파티션|예|예, 최대 3|||||예|  
|자동 관리 캐싱|예||||||예|  
|사용자 지정 어셈블리(저장 프로시저)|예|예|||||사용자 계정 컨트롤|  
|MDX 쿼리 및 스크립트|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|DAX 쿼리|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|역할 기반 보안 모델|사용자 계정 컨트롤|예|||||예|  
|차원 및 셀 수준 보안|예|예|||||사용자 계정 컨트롤|  
|확장 가능 문자열 스토리지|사용자 계정 컨트롤|예|||||예|  
|MOLAP, ROLAP 및 HOLAP 스토리지 모델|예|예|||||사용자 계정 컨트롤|  
|이진 및 압축 XML 전송|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|밀어넣기 모드 처리|사용자 계정 컨트롤||||||예|  
|측정값 식|예||||||예|  
  
 <sup>1</sup> Standard Edition에서 LastChild 반가산적 측정값은 지원되지만 None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren 및 ByAccount와 같은 다른 반가산적 측정값은 지원되지 않습니다. Sum, Count, Min, Max와 같은 가산적 측정값과 비가산적 측정값(DistinctCount)은 모든 버전에서 지원됩니다.  
  <sup>2</sup> Standard Edition에서는 동일한 데이터베이스 내에서 측정값 및 차원 연결이 지원되지만 다른 데이터베이스 또는 인스턴스에서는 지원되지 않습니다.
  
## <a name="power-pivot-for-sharepoint"></a>SharePoint용 PowerPivot  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|공유 서비스 아키텍처를 기반으로 하는 SharePoint 팜 통합|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|사용 보고|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|상태 모니터링 규칙|사용자 계정 컨트롤||||||예|  
|파워 피벗 갤러리|예||||||예|  
|파워 피벗 데이터 새로 고침|예||||||예|  
|파워 피벗 데이터 피드|예||||||예|  
  
## <a name="data-mining"></a>데이터 마이닝  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|표준 알고리즘|예|예|||||예|  
|데이터 마이닝 도구(마법사, 편집기, 쿼리 작성기)|예|예|||||예|  
|교차 유효성 검사|예||||||예|  
|마이닝 구조 데이터의 필터링된 하위 집합에 대한 모델|예||||||사용자 계정 컨트롤|  
|시계열: ARTXP 및 ARIMA 방식 간의 사용자 지정 혼합|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|시계열: 새 데이터를 사용한 예측|사용자 계정 컨트롤||||||예|  
|무제한 동시 DM 쿼리|예||||||예|  
|데이터 마이닝 알고리즘용 고급 구성 및 튜닝 옵션|예||||||사용자 계정 컨트롤|  
|플러그 인 알고리즘 지원|사용자 계정 컨트롤||||||예|  
|병렬 모델 처리|예||||||예|  
|시계열: 계열 간 예측|예||||||예|  
|연결 규칙에 대한 무제한 특성|예||||||예|  
|시퀀스 예측|예||||||예|  
|naïve Bayes, 신경망, 로지스틱 회귀 분석을 위한 다중 예측 대상|예||||||사용자 계정 컨트롤|  
  


