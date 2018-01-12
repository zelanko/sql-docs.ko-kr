---
title: "OLAP 큐브에서 데이터를 사용 하 여 R에서 | Microsoft Docs"
ms.custom: 
ms.date: 12/08/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: 
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: e8aa8d51c54fb98b3851676ddedd367f476dd1fa
ms.sourcegitcommit: 06131936f725a49c1364bfcc2fccac844d20ee4d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
# <a name="using-data-from-olap-cubes-in-r"></a>OLAP 큐브에서 데이터를 사용 하 여 R에서

**olapR** 패키지에 R 패키지가 제공 됩니다 컴퓨터 학습 서버와 SQL Server와 함께 사용할 microsoft에서 OLAP 큐브에서 데이터를 가져오려면 MDX 쿼리를 실행할 수 있습니다. 이 패키지와 연결 된 서버를 만들거나 평면화 된 행 집합; 정리 필요 하지 않습니다. 오른쪽에서 직접 OLAP 데이터를 가져올 수 있습니다.

이 문서에서는 다차원 큐브 데이터베이스를 처음 사용 될 수 있는 R 사용자에 대 한 OLAP 및 MDX의 개요와 함께 API를 설명 합니다.

> [!IMPORTANT]
> Analysis Services의 인스턴스 기존의 다차원 큐브 또는 테이블 형식 모델을 지원할 수 있지만 인스턴스는 두 가지 유형의 모델을 지원할 수 없습니다. 따라서 있는 큐브에 대해 MDX 쿼리를 작성 하려고 하기 전에 Analysis Services 인스턴스의 다차원 모델 포함 되어 있는지 확인 합니다.

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

    SSMS 또는 Excel 등의 모든 클라이언트 유틸리티를 사용 하 여 MDX를 빌드한 후 쿼리 문자열을 저장 합니다. 이 MDX 문자열에 대 한 인수로 제공 된 *SSAS 쿼리 처리기* 에 **olapR** 패키지 합니다. 공급자가 지정된 된 Analysis Services 서버에 쿼리를 보내고 오른쪽으로 결과 다시 전달 

MDX를 작성 하는 방법의 예는 쿼리 또는 기존 MDX 쿼리를 실행, 참조 [R을 사용 하 여 MDX 쿼리를 만드는 방법을](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)합니다.

## <a name="known-issues"></a>알려진 문제

이 섹션에서는 몇 가지 알려진된 문제 및 관련 된 일반적인 질문에 대 한 설명의 **olapR** 패키지 합니다.

### <a name="tabular-model-support"></a>테이블 형식 모델 지원

테이블 형식 모델에 포함 된 Analysis Services의 인스턴스에 연결 하는 `explore` 함수는 반환 값 true 이면 성공한 것으로 보고 합니다. 그러나 테이블 형식 모델 개체 다차원 개체와 다르며 다차원 데이터베이스의 구조는 테이블 형식 모델의 다릅니다.

DAX (데이터 분석 식)은 일반적으로 테이블 형식 모델과 함께 사용 되는 언어를 MDX를 사용 하 던 하는 경우 테이블 형식 모델에 대 한 유효한 MDX 쿼리를 디자인할 수 있습니다. 테이블 형식 모델에 대 한 유효한 MDX 쿼리를 작성할 때 olapR 생성자를 사용할 수 없습니다.

그러나 MDX 쿼리는 테이블 형식 모델에서 데이터를 검색 하는 비효율적인 방법입니다. R에서 사용 하기 위해 테이블 형식 모델에서 데이터를 가져올 해야 할 경우 이러한 메서드를 대신 고려 합니다.

+ 모델에서 DirectQuery를 사용 하도록 설정 하 고 SQL Server에 연결 된 서버로 서버를 추가 합니다. 
+ 테이블 형식 모델이 관계형 데이터 마트 빌드된, 소스에서 직접 데이터를 가져옵니다.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>인스턴스 테이블 형식 또는 다차원 모델에 포함 되는지 여부를 확인 하는 방법

단일 Analysis Services 인스턴스에 여러 모델을 포함할 수 있지만 한 가지 유형의 모델을 포함할 수 있습니다. 원인은 테이블 형식 모델 및 데이터 저장 및 처리 되는 방식을 제어 하는 다차원 모델 간의 근본적인 차이가 있습니다. 예를 들어 테이블 형식 모델은 메모리에 저장 및 columnstore 인덱스는 매우 빠른 계산을 수행 하도록 활용 합니다. 다차원 모델의 데이터는 디스크에 저장 및 집계는 미리 정의 및 MDX 쿼리를 사용 하 여 검색 합니다.

SQL Server Management Studio와 같은 클라이언트를 사용 하 여 Analysis Services에 연결 하면 알 수 있습니다를 한 눈에는 데이터베이스에 대 한 아이콘을 확인 하 여 모델 유형을 지원 됩니다.

볼 수 있으며 어떤 유형의 모델 인스턴스가 지원 결정 하는 서버 속성을 쿼리할 수도 있습니다. **서버 모드** 속성 두 값을 지원: _다차원_ 또는 _테이블 형식_합니다.

두 가지 유형의 모델에 대 한 일반적인 내용은 다음 문서를 참조 합니다.

+ [다차원 및 테이블 형식 모델 비교](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

서버 속성을 쿼리 하는 방법에 대 한 내용은 다음 문서를 참조 하십시오.

+ [OLAP 스키마 행 집합 용 OLE DB](https://docs.microsoft.com/sql/analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>쓰기 저장이 지원 되지 않습니다.

큐브에 사용자 지정 R 계산의 결과 다시 작성 하는 것이 불가능 합니다.

일반적으로 큐브 쓰기 저장을 사용 하도록 구성 되어 있는 경우에 제한 된 작업만 지원 되며 추가 구성이 필요할 수 있습니다. 이러한 작업에 대 한 MDX를 사용 하는 것이 좋습니다.

+ [쓰기 가능 차원](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [쓰기 가능 파티션](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [셀 데이터에 사용자 지정 액세스 설정](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>큐브 처리를 차단 하는 장기 실행 MDX 쿼리

하지만 **olapR** 패키지만 읽기 작업을 수행 장기 실행 MDX 쿼리는 큐브가 처리 되지 않도록 방지 하는 잠금을 만들 수 있습니다. 항상 테스트 MDX 쿼리 사전에 반환 해야 하는 데이터 양과 알 수 있도록 합니다.

잠겨 있는 큐브에 연결 하려고 하면 SQL Server 데이터 웨어하우스를 연결할 수 없는 오류가 발생할 수 있습니다. 제안 된 해결 방법은 다음과 서버 또는 인스턴스 이름 및 등; 검사 하는 원격 연결을 사용 그러나 이전 열린 연결 될 가능성을 고려 합니다.

SSAS 관리자 방지할 수를 식별 하 고 열려 있는 세션을 종료 하 여 잠금 문제가 있습니다. 또한 MDX 쿼리에서 모든 장기 실행 쿼리를 강제로 종료 하는 서버 수준에서 timeout 속성을 적용할 수 있습니다.

## <a name="resources"></a>리소스

Olap 또는 MDX 쿼리를 처음 이라면 다음 Wikipedia 문서를 참조 합니다. 

+ [OLAP 큐브](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 쿼리](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
