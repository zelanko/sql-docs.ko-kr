---
title: "OLAP 큐브에서 데이터를 사용 하 여 R에서 | Microsoft Docs"
ms.custom: 
ms.prod: sql-non-specified
ms.date: 11/29/2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: r-services
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 60e95f4c101a4afe2a8161ba40df7b27bd85f602
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>OLAP 큐브에서 데이터를 사용 하 여 R에서

**olapR** 패키지에 R 패키지가 제공 됩니다 컴퓨터 학습 서버와 SQL Server와 함께 사용할 microsoft에서 OLAP 큐브에서 데이터를 가져오려면 MDX 쿼리를 실행할 수 있습니다. 이 패키지와 연결 된 서버를 만들거나 평면화 된 행 집합; 정리 필요 하지 않습니다. OLAP 데이터를 사용 하 여 R에서 직접

이 문서에서는 다차원 큐브 데이터베이스를 처음 사용 될 수 있는 R 사용자에 대 한 OLAP 및 MDX의 개요와 함께 API를 설명 합니다.

> [!IMPORTANT]
> Analysis Services의 인스턴스 기존의 다차원 큐브 또는 테이블 형식 모델을 지원할 수 있지만 인스턴스는 두 가지 유형의 모델을 지원할 수 없습니다. 따라서 Analysis Services 데이터베이스에 대 한 쿼리를 만들기 전에 다차원 모델에 포함 되어 있는지 확인 합니다.
> 
> MDX를 사용 하 여 테이블 형식 모델을 쿼리할 수 있지만 **olapR** 패키지는 인스턴스가 테이블 형식 모델에 대 한 연결을 지원 하지 않습니다. 더 나은 옵션은 사용할 수 있도록 테이블 형식 모드에서 데이터를 가져오는 해야 할 경우 [DirectQuery](https://docs.microsoft.com/sql/analysis-services/tabular-models/directquery-mode-ssas-tabular) 모델과 SQL Server에 연결 된 서버로 사용할 수 있는 인스턴스 만들기에 있습니다. 

## <a name="what-is-an-olap-cube"></a>OLAP 큐브는 무엇입니까?

OLAP은 짧은 온라인 분석 처리 합니다. OLAP 솔루션 캡처 및 시간에 따라 중요 한 비즈니스 데이터를 저장 하기 위한 광범위 하 게 사용 됩니다. OLAP 데이터는 다양한 도구, 대시보드 및 시각화에서 비즈니스 분석에 사용됩니다. 자세한 내용은 참조 [온라인 분석 처리](https://en.wikipedia.org/wiki/Online_analytical_processing)합니다.

Microsoft 제공 [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), 디자인, 배포 하 고 OLAP 데이터 형식으로 쿼리할 수 있는 _큐브_ 또는 _테이블 형식 모델_합니다. 큐브는 다차원 데이터베이스. _차원_ 차원을 사용 하 여 데이터를 요약 하거나 분석할의 일부 특정 하위 집합을 식별 하는 데이터 또는 r에서 요소 패싯 유사 합니다. 예를 들어 시간은 기본적으로 분리 하 고 데이터를 요약 하는 경우 사용 하도록 정의 된 여러 개의 달력을 포함 하는 대부분 OLAP 솔루션 있도록 정도로 중요 한 차원입니다. 

성능상의 이유로 OLAP 데이터베이스는 종종 계산 요약 (또는 _집계_) 사전에 빠른 검색을 위해 저장 합니다. 요약에 기반 *측정값*를 나타내는 숫자 데이터에 적용할 수 있는 수식입니다. 차원을 사용 하 여 데이터의 하위 집합을 정의 하 고 해당 데이터에 대해 측정값을 계산 합니다. 예를 들어 특정 공급 업체, 연도-날짜까지 누적 임금 유료, 등에 대 한 평균 운송 비용을 보고 하는 세금을 뺀 여러 분기 동안 특정 제품 라인에 대 한 총 판매액을 계산 하는 측정값을 사용 합니다.

MDX, 짧은 다차원 식에는 큐브를 쿼리 하는 데 언어입니다. MDX 쿼리는 일반적으로 MDX 쿼리를 가져와서 훨씬 더 복잡 하는 롤링 windows, 누적 평균, 합계, 순위, 또는 백분위 수를 포함 하지만 하나 이상의 차원과 하나 이상의 측정값을 포함 하는 데이터 정의 포함 합니다. 

MDX 쿼리 작성을 시작 하면 도움이 될 수 있는 몇 가지 다른 용어는 다음과 같습니다.

+ *조각화* 단일 차원 값을 사용 하 여 큐브의 하위 집합을 사용 합니다.

+ *분할* 여러 차원에서 값의 범위를 지정하여 하위 큐브를 만듭니다.

+ *드릴다운* 요약에서 세부 정보로 탐색합니다.

+ *드릴업* 세부 정보에서 더 높은 수준의 집계로 이동합니다.

+ *롤업* 한 차원에 데이터를 요약합니다.

+ *피벗* 큐브 또는 데이터 선택을 회전합니다.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>MDX 쿼리를 만드는 olapR를 사용 하는 방법

다음 문서를 작성 하거나 큐브에 대 한 쿼리를 실행 하는 구문은의 자세한 예제를 제공 합니다.

+ [R을 사용 하 여 MDX 쿼리를 만드는 방법](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 패키지는 MDX 쿼리를 만드는 두 가지 방법을 지원합니다.

- **MDX 작성기를 사용 합니다.** 패키지에 R 함수를 사용 하 여 큐브를 선택 하 고 다음 축 및 슬라이서를 설정 하 여 간단한 MDX 쿼리를 생성 합니다. 이 쉽게 기존 OLAP 도구에 액세스할 수 없는 또는 MDX 언어의 대 한 깊은 지식이 없는 경우에 유효한 MDX 쿼리를 작성할 수 있습니다.

    모든 MDX 쿼리에 MDX 복잡할 수 있으므로이 방법을 사용 하 여 만들 수 있습니다. 그러나이 API는 대부분의 조각, 분할, 드릴 다운, rollup 및 피벗 N 차원에 포함 하는 가장 일반적이 고 유용 작업을 지원 합니다.

+ **잘 구성 된 MDX 복사-붙여넣기 합니다.** 수동으로 만들고 모든 MDX 쿼리에 붙여 넣습니다. 빌드 하려는 쿼리가 너무 복잡 하는 경우 또는 기존 MDX 쿼리를 다시 사용 하려는 경우이 옵션은 가장 적합 한 **olapR** 처리 하도록 합니다. 

    SSMS 또는 Excel 등의 모든 클라이언트 유틸리티를 사용 하 여 MDX 빌드하고 MDX 쿼리를 정의 하는 문자열을 저장 합니다. 이 MDX 문자열에 대 한 인수로 제공한는 *SSAS 쿼리 처리기* 에 **olapR** 패키지 합니다. 지정 된 Analysis Services 서버에 쿼리를 전송 하 고 R, 물론 큐브를 쿼리 하는 권한이 있는 것으로 가정 하 고 그 결과 다시 전달 합니다.

MDX를 작성 하는 방법의 예는 쿼리 또는 기존 MDX 쿼리를 실행, 참조 [R을 사용 하 여 MDX 쿼리를 만드는 방법을](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)합니다.

## <a name="known-issues"></a>알려진 문제

이 섹션에서는 몇 가지 알려진된 문제 및 관련 된 일반적인 질문에 대 한 설명의 **olapR** 패키지 합니다.

### <a name="tabular-models-are-not-supported"></a>테이블 형식 모델이 지원 되지 않습니다.

테이블 형식 모델에 포함 된 Analysis Services의 인스턴스에 연결 하는 `explore` 함수는 반환 값 true 이면 성공한 것으로 보고 합니다. 그러나 테이블 형식 모델 개체 호환 되는 유형 않으며 탐색할 수 없습니다.

또한 (외부 도구를 사용)에서 테이블 형식 모델에 대 한 유효한 MDX 쿼리를 디자인 하 고이 API에는 쿼리를 붙여 경우 쿼리는 NULL 결과 반환 되며 오류를 보고 하지 않습니다.

R에서 사용 하기 위해 테이블 형식 모델에서 데이터를 추출 해야 할 경우이 옵션을 고려해 보십시오.

+ 모델에서 DirectQuery를 사용 하도록 설정 하 고 SQL Server에 연결 된 서버로 서버를 추가 합니다. 
+ 테이블 형식 모델이 관계형 데이터 마트 빌드된, 소스에서 직접 데이터를 가져옵니다.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>인스턴스 테이블 형식 또는 다차원 모델에 포함 되는지 여부를 확인 하는 방법

테이블 형식 모델 간의 근본적인 차이점 있으며 방식으로 데이터에 영향을 주는 다차원 모델 저장 및 처리 됩니다. 예를 들어 테이블 형식 모델은 메모리에 저장 및 columnstore 인덱스는 매우 빠른 계산을 수행 하도록 활용 합니다. 다차원 모델의 데이터는 디스크에 저장 및 집계는 미리 정의 및 MDX 쿼리를 사용 하 여 검색 합니다.

이러한 이유로 단일 Analysis Services 인스턴스는 한 가지 유형의 모델을 포함할 수 있습니다. 다음 문서를 두 가지 유형의 모델을 구별 하는 방법에 대 한 자세한 설명에 대 한 참조.

+ [다차원 및 테이블 형식 모델 비교](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

SQL Server Management Studio와 같은 클라이언트를 사용 하 여 Analysis Services에 연결 하면 알 수 있습니다를 한 눈에는 데이터베이스에 대 한 아이콘을 확인 하 여 모델 유형을 지원 됩니다.

또한 서버 속성을 볼 수 있습니다. **서버 모드** 속성 두 값을 지원: _다차원_ 또는 _테이블 형식_합니다.

서버 속성을 사용 하 여 서버 유형을 확인 하는 방법에 대 한 자세한 내용은 참조 [OLAP 스키마 행 집합 용 OLE DB](https://docs.microsoft.com/sql/analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>쓰기 저장이 지원 되지 않습니다.

큐브에 사용자 지정 R 계산의 결과 다시 작성 하는 것이 불가능 합니다.

일반적으로 큐브 쓰기 저장을 사용 하도록 구성 되어 있는 경우에 제한 된 작업만 지원 되며 추가 구성이 필요할 수 있습니다. 이러한 작업에 대 한 MDX를 사용 하는 것이 좋습니다.

+ [쓰기 가능 차원](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [쓰기 가능 파티션](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [셀 데이터에 사용자 지정 액세스 설정](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

## <a name="resources"></a>리소스

Olap 또는 MDX 쿼리를 처음 이라면 다음 Wikipedia 문서를 참조 합니다. 

+ [OLAP 큐브](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 쿼리](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
