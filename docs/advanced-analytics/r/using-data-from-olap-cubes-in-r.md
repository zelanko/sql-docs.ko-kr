---
title: "OLAP 큐브에서 데이터를 사용 하 여 R에서 | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1c55a5b834cd91478a87ded7ebb86884117c7bfb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>OLAP 큐브에서 데이터를 사용 하 여 R에서

**olapR** 패키지에 R 패키지가 제공 됩니다 학습 서버 컴퓨터와 SQL Server R Services 사용 하기 위해 microsoft에서 OLAP 큐브 데이터를 가져오려면 MDX 쿼리를 실행할 수 있습니다. 이 패키지와 연결 된 서버를 만들거나 평면화 된 행 집합; 정리 필요 하지 않습니다. OLAP 데이터를 사용 하 여 R에서 직접

이 문서에서는 개요와 함께 API 설명 fo OLAP 및 다차원 큐브 데이터베이스를 처음 사용 될 수 있는 R 사용자에 대 한 MDX 합니다.

## <a name="what-is-an-olap-cube"></a>OLAP 큐브는 무엇입니까?

OLAP은 짧은 온라인 분석 처리 합니다. OLAP 솔루션 캡처 및 시간에 따라 중요 한 비즈니스 데이터를 저장 하기 위한 광범위 하 게 사용 됩니다. OLAP 데이터는 다양한 도구, 대시보드 및 시각화에서 비즈니스 분석에 사용됩니다. 자세한 내용은 참조 [온라인 분석 처리](https://en.wikipedia.org/wiki/Online_analytical_processing)합니다.

Microsoft 제공 [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), 디자인, 배포 하 고 OLAP 데이터 형식으로 쿼리할 수 있는 _큐브_ 또는 _테이블 형식 모델_합니다. 큐브는 다차원 데이터베이스. _차원_ 차원을 사용 하 여 데이터를 요약 하거나 분석할의 일부 특정 하위 집합을 식별 하는 데이터 또는 r에서 요소 패싯 유사 합니다. 예를 들어 시간은 기본적으로 분리 하 고 데이터를 요약 하는 경우 사용 하도록 정의 된 여러 개의 달력을 포함 하는 대부분 OLAP 솔루션 있도록 정도로 중요 한 차원입니다. 

성능상의 이유로 OLAP 데이터베이스는 종종 계산 요약 (또는 _집계_) 사전에 빠른 검색을 위해 저장 합니다. 요약에 기반 *측정값*를 나타내는 숫자 데이터에 적용할 수 있는 수식입니다. 차원을 사용 하 여 데이터의 하위 집합을 정의 하 고 해당 데이터에 대해 측정값을 계산 합니다. 예를 들어 특정 공급 업체, 연도-날짜까지 누적 임금 유료, 등에 대 한 평균 운송 비용을 보고 하는 세금을 뺀 여러 분기 동안 특정 제품 라인에 대 한 총 판매액을 계산 하는 측정값을 사용 합니다.

MDX, 짧은 다차원 식에는 큐브를 쿼리 하는 데 언어입니다. MDX 쿼리는 일반적으로 하나 이상의 차원과 하나 이상의 측정값을 포함 하는 데이터 정의 포함, thogh MDX 쿼리를 가져와서 훨씬 더 복잡 하는 windows, 누적 평균 또는 합계, 백분위 수를 롤링 포함 합니다. 

MDX 쿼리 작성을 시작 하면 도움이 될 수 있는 몇 가지 다른 용어는 다음과 같습니다.

+ *조각화* 단일 차원 값을 사용 하 여 큐브의 하위 집합을 사용 합니다.

+ *분할* 여러 차원에서 값의 범위를 지정하여 하위 큐브를 만듭니다.

+ *드릴다운* 요약에서 세부 정보로 탐색합니다.

+ *드릴업* 세부 정보에서 더 높은 수준의 집계로 이동합니다.

+ *롤업* 한 차원에 데이터를 요약합니다.

+ *피벗* 큐브 또는 데이터 선택을 회전합니다.

이 항목에 큐브에 대 한 쿼리 추가 예제를는 기본 구문 제공합니다. 

+ [R을 사용 하 여 MDX 쿼리를 만드는 방법](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 패키지는 MDX 쿼리를 만드는 두 가지 방법을 지원합니다.

- **MDX 작성기를 사용 합니다.** 패키지의 R 함수를 사용 하 여 큐브 및 설정 축 및 슬라이서를 선택 하 여 간단한 MDX 쿼리를 생성 합니다. 이 쉽게 기존 OLAP 도구에 액세스할 수 없는 또는 MDX 언어의 대 한 깊은 지식이 없는 경우에 유효한 MDX 쿼리를 작성할 수 있습니다.

    가능한 모든 MDX 쿼리에 MDX 복잡할 수 있으므로이 방법을 사용 하 여 만들 수 있습니다. 그러나이 API는 대부분의 조각, 분할, 드릴 다운, rollup 및 피벗 N 차원에 포함 하는 가장 일반적이 고 유용 작업을 지원 합니다.

+ **잘 구성 된 MDX 복사-붙여넣기 합니다.** 수동으로 만들고 모든 MDX 쿼리에 붙여 넣습니다. 빌드 하려는 쿼리가 너무 복잡 하는 경우 또는 기존 MDX 쿼리를 다시 사용 하려는 경우이 옵션은 가장 적합 한 **olapR** 처리 하도록 합니다. 

    SSMS 또는 Excel 등의 모든 클라이언트 유틸리티를 사용 하 여 MDX 빌드하고 MDX 쿼리를 정의 하는 문자열을 저장 합니다. 이 MDX 문자열에 대 한 인수로 제공한는 *SSAS 쿼리 처리기* 에 **olapR** 패키지 합니다. 지정 된 Analysis Services 서버에 쿼리를 전송 하 고 R, 물론 큐브를 쿼리 하는 권한이 있는 것으로 가정 하 고 그 결과 다시 전달 합니다.

MDX를 작성 하는 방법의 예는 쿼리 또는 기존 MDX 쿼리를 실행, 참조 [R을 사용 하 여 MDX 쿼리를 만드는 방법을](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)합니다.

## <a name="known-issues"></a>알려진 문제

### <a name="tabular-models-not-supported"></a>테이블 형식 모델 지원 되지 않습니다

+ Analysis Services의 테이블 형식 인스턴스에 연결 하는 `explore` 함수는 반환 값 true 이면 성공한 것으로 보고 합니다. 그러나 테이블 형식 모델 개체 호환 되는 유형 않으며 탐색할 수 없습니다.

+ 테이블 형식 모델은 DAX 또는 MDX를 사용 하 여 쿼리할 수 있습니다. 외부 도구를 사용 하 여 테이블 형식 모델에 대 한 유효한 MDX 쿼리를 디자인 하 고이 API에는 쿼리를 붙여 경우 쿼리 NULL 결과 반환 되며 오류를 보고 하지 않습니다.

## <a name="resources"></a>리소스

OLAP 또는 MDX 쿼리를 처음 사용하는 경우 Wikipedia 문서 [OLAP Cubes](https://en.wikipedia.org/wiki/OLAP_cube)
[MDX queries](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>샘플

큐브에 대해 자세히 알아보려면 Analysis Services 자습서의 4단원 [OLAP 큐브 만들기](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)까지 수행하여 이러한 예제에서 사용되는 큐브를 만들 수 있습니다.

기존 큐브를 백업으로 다운로드하여 Analysis Services의 인스턴스로 복원할 수도 있습니다. 예를 들어 [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)(Adventure Works 다차원 모델 SQL 2014)의 완전히 처리된 큐브를 압축된 형식으로 다운로드하여 SSAS 인스턴스로 복원할 수 있습니다. 자세한 내용은 [백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md), 또는 [Restore-ASDatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)을 참조하세요.
