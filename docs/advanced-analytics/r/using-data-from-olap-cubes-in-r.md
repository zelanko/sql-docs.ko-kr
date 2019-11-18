---
title: R에서 OLAP 큐브의 데이터 사용
description: 이 문서에서는 다차원 큐브 데이터베이스를 처음 접하는 사용자를 위한 OLAP 및 MDX 개요와 함께 olapR API에 대해 설명합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2da5cbf0fd3fbc5b8fe1105261fff98625d590e5
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727318"
---
# <a name="using-data-from-olap-cubes-in-r"></a>R에서 OLAP 큐브의 데이터 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR** 패키지는 Machine Learning Server 및 SQL Server와 함께 사용하도록 Microsoft에서 제공하는 R 패키지로, MDX 쿼리를 실행하여 OLAP 큐브에서 데이터를 가져올 수 있습니다. 이 패키지를 사용하면 연결된 서버를 만들거나 일반 행 세트를 정리할 필요가 없으며, R에서 직접 OLAP 데이터를 가져올 수 있습니다.

이 문서에서는 다차원 큐브 데이터베이스를 처음 접하는 사용자를 위한 OLAP 및 MDX 개요와 함께 API에 대해 설명합니다.

> [!IMPORTANT]
> Analysis Services 인스턴스는 전통적인 다차원 큐브 또는 테이블 형식 모델을 지원할 수 있지만, 인스턴스는 두 가지 유형의 모델을 모두 지원할 수 없습니다. 따라서 큐브에 대한 MDX 쿼리를 작성하기 전에, Analysis Services 인스턴스에 다차원 모델이 포함되어 있는지 확인해야 합니다.

## <a name="what-is-an-olap-cube"></a>OLAP 큐브란?

OLAP은 온라인 분석 처리의 약어입니다. OLAP 솔루션은 시간에 따라 중요한 비즈니스 데이터를 캡처하고 저장하는 데 광범위하게 사용됩니다. OLAP 데이터는 다양한 도구, 대시보드 및 시각화에서 비즈니스 분석에 사용됩니다. 자세한 내용은 [온라인 분석 처리](https://en.wikipedia.org/wiki/Online_analytical_processing)를 참조하세요.

Microsoft는 _큐브_ 또는 _테이블 형식 모델_의 형태로 OLAP 데이터를 디자인, 배포 및 쿼리할 수 있는 [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)를 제공합니다. 큐브는 다차원 데이터베이스입니다. _차원_은 데이터의 패싯 또는 R의 요소와 비슷합니다. 차원을 사용하여 요약 또는 분석할 데이터의 특정 하위 세트를 식별할 수 있습니다. 예를 들어 시간은 중요한 차원이므로, 대부분의 OLAP 솔루션은 데이터를 분리하고 요약할 때 사용할 수 있도록 기본적으로 정의된 여러 달력을 포함하고 있습니다. 

성능상의 이유로, OLAP 데이터베이스가 요약(또는 _집계_)을 미리 계산한 다음, 더 빠른 검색을 위해 요약을 저장하는 경우가 종종 있습니다. 요약은 숫자 데이터에 적용할 수 있는 수식을 나타내는 *측정값*를 기반으로 합니다. 차원을 사용하여 데이터의 하위 세트를 정의한 다음, 해당 데이터를 대상으로 측정값을 컴퓨팅합니다. 예를 들어 측정값을 사용하여 여러 분기 동안 판매된 특정 제품 라인의 총 매출에서 세금을 제한 금액을 컴퓨팅하고, 특정 공급업체의 평균 배송 비용, 올해 초부터 현재까지 지급된 누적 임금 등을 보고할 수 있습니다.

Multidimensional Expression의 약어인 MDX는 큐브를 쿼리하는 데 사용되는 언어입니다. MDX 쿼리는 훨씬 복잡한 데이터 정의를 포함할 수 있지만 일반적으로는 하나 이상의 차원과 하나 이상의 측정값이 들어 있는 데이터 정의를 포함하고 있으며 이동 기간, 누적 평균, 합계, 순위 또는 백분위수를 포함할 수 있습니다. 

다음은 MDX 쿼리 작성을 시작할 때 도움이 될 만한 몇 가지 다른 용어입니다.

+ *조각화*란 단일 차원의 값을 사용하여 큐브의 하위 세트를 가져오는 것입니다.

+ *분할* 여러 차원에서 값의 범위를 지정하여 하위 큐브를 만듭니다.

+ *드릴다운* 요약에서 세부 정보로 탐색합니다.

+ *드릴업* 세부 정보에서 더 높은 수준의 집계로 이동합니다.

+ *롤업* 한 차원에 데이터를 요약합니다.

+ *피벗* 큐브 또는 데이터 선택을 회전합니다.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>olapR을 사용하여 MDX 쿼리를 만드는 방법

다음 문서에서는 큐브에 대해 쿼리를 만들거나 실행하는 구문의 자세한 예를 제공합니다.

+ [R을 사용하여 MDX 쿼리를 만드는 방법](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 패키지는 MDX 쿼리를 만드는 두 가지 방법을 지원합니다.

- **MDX 작성기를 사용합니다.** 패키지의 R 함수를 사용하여 간단한 MDX 쿼리를 생성합니다. 큐브를 선택한 다음, 축과 슬라이서를 설정하면 됩니다. 기존의 OLAP 도구에 액세스할 수 없거나 MDX 언어에 대한 깊은 지식이 없어도 이와 같은 간단한 방법으로 유효한 MDX 쿼리를 작성할 수 있습니다.

    MDX가 복잡할 수 있으므로, 모든 MDX 쿼리를 이 방법으로 만들 수는 없습니다. 그러나 이 API는 N 차원에서 조각화, 분석, 드릴다운, 롤업, 피벗 등 가장 일반적이고 유용한 대부분의 작업을 지원합니다.

+ **잘 구성된(Well-Formed) MDX를 복사하여 붙여넣습니다.** 수동으로 MDX 쿼리를 만들어서 붙여넣습니다. 이 옵션은 다시 사용하려는 기존 MDX 쿼리가 있는 경우 또는 작성하려는 쿼리가 너무 복잡하여 **olapR**에서 처리할 수 없는 경우에 가장 적합합니다.

    SSMS 또는 Excel 같은 클라이언트 유틸리티를 사용하여 MDX를 빌드한 후에는 쿼리 문자열을 저장합니다. 이 MDX 문자열을 **olapR** 패키지의 *SSAS 쿼리 처리기*에 인수로 제공합니다. 공급자는 이 쿼리를 지정된 Analysis Services 서버로 보내고, 그 결과를 다시 R에 전달합니다. 

MDX 쿼리를 작성하거나 기존 MDX 쿼리를 실행하는 방법에 대한 예는 [R을 사용하여 MDX 쿼리를 만드는 방법](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)을 참조하세요.

## <a name="known-issues"></a>알려진 문제

이 섹션에서는 **olapR** 패키지와 관련된 몇 가지 알려진 문제 및 일반적인 질문을 보여줍니다.

### <a name="tabular-model-support"></a>테이블 형식 모델 지원

테이블 형식 모델이 들어 있는 Analysis Services 인스턴스에 연결하면 `explore` 함수는 반환 값 TRUE와 함께 성공을 보고합니다. 그러나 테이블 형식 모델 개체는 다차원 개체와 다르며, 다차원 데이터베이스의 구조는 테이블 형식 모델의 구조와 다릅니다.

DAX(Data analysis Expressions)는 일반적으로 테이블 형식 모델에 사용되는 언어이지만, 이미 MDX에 익숙한 경우에는 테이블 형식 모델에 대한 유효한 MDX 쿼리를 디자인할 수 있습니다. olapR 생성자를 사용하여 테이블 형식 모델에 대한 유효한 MDX 쿼리를 작성할 수는 없습니다.

그러나 MDX 쿼리는 테이블 형식 모델에서 데이터를 검색하는 비효율적인 방법입니다. R에서 사용하기 위해 테이블 형식 모델에서 데이터를 가져와야 하는 경우 다음 방법을 사용하는 것이 좋습니다.

+ 모델에서 DirectQuery를 사용하도록 설정하고 서버를 SQL Server에서 연결된 서버로 추가합니다. 
+ 테이블 형식 모델이 관계형 데이터 마트에 빌드된 경우 원본에서 직접 데이터를 가져옵니다.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>인스턴스에 테이블 형식 모델 또는 다차원 모델이 들어 있는지 확인하는 방법

단일 Analysis Services 인스턴스는 한 종류의 모델만 포함할 수 있지만, 여러 개의 모델을 포함할 수 있습니다. 테이블 형식 모델과 다차원 모델은 데이터를 저장하고 처리하는 방식이 근본적으로 다르기 때문입니다. 예를 들어 테이블 형식 모델은 메모리에 저장되며, columnstore 인덱스를 활용하여 매우 빠른 계산을 수행합니다. 다차원 모델에서는 데이터가 디스크에 저장되며, 집계는 MDX 쿼리를 사용하여 미리 정의되고 검색됩니다.

SQL Server Management Studio 같은 클라이언트를 사용하여 Analysis Services에 연결하는 경우 데이터베이스 아이콘만 보면 어떤 모델 유형이 지원되는지 바로 알 수 있습니다.

서버 속성을 보고 쿼리하여 인스턴스에서 지원하는 모델 유형을 확인할 수도 있습니다. **서버 모드** 속성은 _다차원_ 또는 _테이블 형식_의 두 가지 값을 지원합니다.

두 가지 모델 유형에 대한 일반적인 내용은 다음 문서를 참조하세요.

+ [다차원 모델과 테이블 형식 모델 비교](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

서버 속성 쿼리에 대한 내용은 다음 문서를 참조하세요.

+ [OLAP용 OLE DB 스키마 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>쓰기 저장은 지원되지 않습니다.

사용자 지정 R 계산 결과를 다시 큐브에 쓸 수는 없습니다.

일반적으로 큐브에 쓰기 저장을 사용하도록 설정된 경우에도 제한된 작업만 지원되며, 추가 구성이 필요할 수도 있습니다. 이러한 작업에는 MDX를 사용하는 것이 좋습니다.

+ [쓰기 가능 차원](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [쓰기 가능 파티션](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [셀 데이터에 대한 사용자 지정 액세스 설정](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>장기 실행 MDX 쿼리는 큐브 처리를 차단

**olapR** 패키지는 읽기 작업만 수행하지만, 장기 실행 MDX 쿼리는 큐브가 처리되는 것을 방지하는 잠금을 만들 수 있습니다. 반환해야 하는 데이터의 양을 알 수 있도록 항상 MDX 쿼리를 미리 테스트하세요.

잠긴 큐브에 연결하려고 시도하면 SQL Server 데이터 웨어하우스에 연결할 수 없다는 오류가 발생할 수 있습니다. 권장하는 해결 방법으로는 원격 연결을 설정하거나 서버 또는 인스턴스 이름을 확인하는 등의 방법이 있지만, 먼저 열려 있는 연결의 가능성을 생각해야 합니다.

SSAS 관리자는 열려 있는 세션을 확인하고 종료하여 잠금 이슈를 방지할 수 있습니다. 서버 수준에서 MDX 쿼리에 시간 제한 속성을 적용하여 모든 장기 실행 쿼리를 강제로 종료할 수도 있습니다.

## <a name="resources"></a>리소스

OLAP 또는 MDX 쿼리를 처음 접하는 경우 다음 Wikipedia 문서를 참조하세요. 

+ [OLAP 큐브](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 쿼리](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
