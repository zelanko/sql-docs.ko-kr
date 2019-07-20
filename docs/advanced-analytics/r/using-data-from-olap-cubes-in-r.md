---
title: R에서 OLAP 큐브의 데이터 사용
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3063758e1186dc81e5ce9e70891403e7afd3a89f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345106"
---
# <a name="using-data-from-olap-cubes-in-r"></a>R에서 OLAP 큐브의 데이터 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**Olapr** 패키지는 Machine Learning Server 및 SQL Server와 함께 사용 하기 위해 Microsoft에서 제공 하는 R 패키지로, OLAP 큐브에서 데이터를 가져오기 위해 MDX 쿼리를 실행할 수 있도록 합니다. 이 패키지를 사용 하면 연결 된 서버를 만들거나 일반 행 집합을 정리할 필요가 없습니다. R에서 직접 OLAP 데이터를 가져올 수 있습니다.

이 문서에서는 다차원 큐브 데이터베이스를 처음 사용 하는 경우의 OLAP 및 MDX 개요와 함께 API에 대해 설명 합니다.

> [!IMPORTANT]
> Analysis Services 인스턴스는 기존 다차원 큐브 또는 테이블 형식 모델을 지원할 수 있지만 인스턴스는 두 가지 유형의 모델을 모두 지원할 수 없습니다. 따라서 큐브에 대해 MDX 쿼리를 작성 하기 전에 Analysis Services 인스턴스에 다차원 모델이 포함 되어 있는지 확인 합니다.

## <a name="what-is-an-olap-cube"></a>OLAP 큐브 란?

OLAP은 온라인 분석 처리에 대해 짧습니다. OLAP 솔루션은 시간별로 중요 한 비즈니스 데이터를 캡처하고 저장 하는 데 널리 사용 됩니다. OLAP 데이터는 다양한 도구, 대시보드 및 시각화에서 비즈니스 분석에 사용됩니다. 자세한 내용은 [온라인 분석 처리](https://en.wikipedia.org/wiki/Online_analytical_processing)를 참조 하세요.

Microsoft는 _큐브_ 또는 _테이블 형식 모델_의 형태로 OLAP 데이터를 디자인, 배포 및 쿼리할 수 있는 [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)을 제공 합니다. 큐브는 다차원 데이터베이스입니다. _차원은_ 데이터의 패싯이 나 R의 요소와 유사 합니다. 차원을 사용 하 여 요약 하거나 분석할 데이터의 특정 하위 집합을 식별 합니다. 예를 들어 time은 중요 한 차원 이므로 대부분의 OLAP 솔루션은 데이터를 분리 하 고 요약할 때 사용할 수 있도록 기본적으로 정의 된 여러 달력을 포함 합니다. 

성능상의 이유로 OLAP 데이터베이스는 요약 또는 _집계_를 미리 계산 하 고 더 빠른 검색을 위해이를 저장 하는 경우가 많습니다. 요약은 숫자 데이터에 적용할 수 있는 수식을 나타내는 *측정값*을 기반으로 합니다. 차원을 사용 하 여 데이터의 하위 집합을 정의한 다음 해당 데이터에 대 한 측정값을 계산 합니다. 예를 들어 측정값을 사용 하 여 여러 분기에서 특정 제품 라인에 대 한 총 판매량을 계산 하 고 특정 공급 업체의 평균 배송 비용, 연간 누계 누적 임금이를 보고할 수 있습니다.

MDX는 MDX를 쿼리 하는 데 사용 되는 언어입니다. Mdx 쿼리는 일반적으로 하나 이상의 차원 및 하나 이상의 측정값을 포함 하는 데이터 정의를 포함 하 고 있습니다. 단, MDX 쿼리는 훨씬 더 복잡 해지고 windows, 누적 평균, 합계, 순위 또는 백분위 수를 포함할 수 있습니다. 

MDX 쿼리 작성을 시작할 때 도움이 될 수 있는 몇 가지 다른 용어는 다음과 같습니다.

+ *조각화* 는 단일 차원의 값을 사용 하 여 큐브의 하위 집합을 사용 합니다.

+ *분할* 여러 차원에서 값의 범위를 지정하여 하위 큐브를 만듭니다.

+ *드릴다운* 요약에서 세부 정보로 탐색합니다.

+ *드릴업* 세부 정보에서 더 높은 수준의 집계로 이동합니다.

+ *롤업* 한 차원에 데이터를 요약합니다.

+ *피벗* 큐브 또는 데이터 선택을 회전합니다.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>OlapR을 사용 하 여 MDX 쿼리를 만드는 방법

다음 문서에서는 큐브에 대해 쿼리를 만들거나 실행 하는 구문에 대 한 자세한 예를 제공 합니다.

+ [R을 사용 하 여 MDX 쿼리를 만드는 방법](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 패키지는 MDX 쿼리를 만드는 두 가지 방법을 지원합니다.

- **MDX 작성기를 사용 합니다.** 패키지의 R 함수를 사용 하 여 큐브를 선택한 다음 축 및 슬라이서를 설정 하 여 간단한 MDX 쿼리를 생성 합니다. 이 방법은 기존 OLAP 도구에 액세스할 수 없거나 MDX 언어에 대 한 심층 지식이 없는 경우 유효한 MDX 쿼리를 작성 하는 쉬운 방법입니다.

    MDX가 복잡할 수 있으므로이 방법을 사용 하 여 일부 MDX 쿼리를 만들 수는 없습니다. 그러나이 API는 N 차원에서 조각, 주사위, 드릴 다운, 롤업 및 피벗을 비롯 하 여 가장 일반적이 고 유용한 작업을 대부분 지원 합니다.

+ **잘 구성 된 MDX를 복사 하 여 붙여넣습니다.** MDX 쿼리를 수동으로 만든 다음 붙여 넣습니다. 이 옵션은 다시 사용 하려는 기존 MDX 쿼리가 있거나 작성 하려는 쿼리가 **Olapr** 에서 처리 하기에 너무 복잡 한 경우에 가장 적합 합니다.

    SSMS 또는 Excel과 같은 클라이언트 유틸리티를 사용 하 여 MDX를 빌드한 후 쿼리 문자열을 저장 합니다. 이 MDX 문자열을 **Olapr** 패키지의 *SSAS 쿼리 처리기* 에 인수로 제공 합니다. 공급자는 지정 된 Analysis Services 서버에 쿼리를 보내고 결과를 R로 다시 전달 합니다. 

MDX 쿼리를 작성 하거나 기존 MDX 쿼리를 실행 하는 방법에 대 한 예는 [R을 사용 하 여 mdx 쿼리를 만드는 방법](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)을 참조 하세요.

## <a name="known-issues"></a>알려진 문제

이 섹션에서는 몇 가지 알려진 문제 및 **Olapr** 패키지에 대 한 일반적인 질문을 나열 합니다.

### <a name="tabular-model-support"></a>테이블 형식 모델 지원

테이블 형식 모델을 포함 하는 Analysis Services 인스턴스에 연결 하는 경우이 함수 `explore` 는 반환 값이 TRUE 인 success를 보고 합니다. 그러나 테이블 형식 모델 개체는 다차원 개체와 다르며 다차원 데이터베이스의 구조는 테이블 형식 모델의 구조와 다릅니다.

DAX (Data analysis Expressions)는 일반적으로 테이블 형식 모델과 함께 사용 되는 언어 이지만 이미 MDX에 익숙한 경우에는 테이블 형식 모델에 대해 유효한 MDX 쿼리를 디자인할 수 있습니다. OlapR 생성자를 사용 하 여 테이블 형식 모델에 대 한 유효한 MDX 쿼리를 작성할 수 없습니다.

그러나 MDX 쿼리는 테이블 형식 모델에서 데이터를 검색 하는 비효율적인 방법입니다. R에서 사용 하기 위해 테이블 형식 모델에서 데이터를 가져와야 하는 경우에는 다음 메서드를 대신 사용 하십시오.

+ 모델에서 DirectQuery를 사용 하도록 설정 하 고 SQL Server에 연결 된 서버로 서버를 추가 합니다. 
+ 관계형 데이터 마트에 테이블 형식 모델을 작성 한 경우 원본에서 직접 데이터를 가져옵니다.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>인스턴스가 테이블 형식 모델 또는 다차원 모델을 포함 하는지 여부를 확인 하는 방법

단일 Analysis Services 인스턴스는 여러 모델을 포함할 수 있지만 모델 유형을 하나만 포함할 수 있습니다. 테이블 형식 모델과 다차원 모델 간에는 데이터가 저장 되 고 처리 되는 방식을 제어 하는 기본적인 차이가 있기 때문입니다. 예를 들어 테이블 형식 모델은 메모리에 저장 되 고 columnstore 인덱스를 활용 하 여 매우 빠른 계산을 수행 합니다. 다차원 모델에서 데이터는 디스크에 저장 되 고 집계는 MDX 쿼리를 사용 하 여 미리 정의 되 고 검색 됩니다.

SQL Server Management Studio와 같은 클라이언트를 사용 하 여 Analysis Services에 연결 하는 경우 데이터베이스에 대 한 아이콘을 확인 하 여 지원 되는 모델 유형을 한눈에 파악할 수 있습니다.

서버 속성을 보고 쿼리하여 인스턴스가 지 원하는 모델 유형을 확인할 수도 있습니다. **서버 모드** 속성은 _다차원_ 또는 _테이블 형식_의 두 값을 지원 합니다.

두 가지 모델 유형에 대 한 일반적인 정보는 다음 문서를 참조 하세요.

+ [다차원 및 테이블 형식 모델 비교](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

서버 속성 쿼리 정보는 다음 문서를 참조 하세요.

+ [OLAP용 OLE DB 스키마 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>쓰기 저장은 지원 되지 않습니다.

사용자 지정 R 계산 결과를 다시 큐브에 쓸 수는 없습니다.

일반적으로 큐브가 쓰기 저장 (writeback)을 사용 하도록 설정 된 경우에도 제한 된 작업만 지원 되며 추가 구성이 필요할 수 있습니다. 이러한 작업에는 MDX를 사용 하는 것이 좋습니다.

+ [쓰기 가능 차원](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [쓰기 가능 파티션](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [셀 데이터에 대 한 사용자 지정 액세스 설정](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>장기 실행 MDX 쿼리는 큐브 처리를 차단 합니다.

**Olapr** 패키지는 읽기 작업만 수행 하지만 장기 실행 MDX 쿼리는 큐브가 처리 되는 것을 방지 하는 잠금을 만들 수 있습니다. 반환 해야 하는 데이터의 양을 알 수 있도록 항상 MDX 쿼리를 미리 테스트 합니다.

잠긴 큐브에 연결 하려고 하면 SQL Server 데이터 웨어하우스에 연결할 수 없다는 오류가 발생할 수 있습니다. 권장 되는 해결 방법으로는 원격 연결을 설정 하 고, 서버 또는 인스턴스 이름을 확인 하는 등이 있습니다. 그러나 이전에 열린 연결의 가능성을 고려해 야 합니다.

SSAS 관리자는 열려 있는 세션을 식별 하 고 종료 하 여 잠금 문제를 방지할 수 있습니다. 시간 제한 속성은 서버 수준의 MDX 쿼리에 적용 되어 모든 장기 실행 쿼리를 강제로 종료할 수도 있습니다.

## <a name="resources"></a>리소스

OLAP 또는 MDX 쿼리를 처음 접하는 경우 다음 위키백과 문서를 참조 하세요. 

+ [OLAP 큐브](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 쿼리](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
