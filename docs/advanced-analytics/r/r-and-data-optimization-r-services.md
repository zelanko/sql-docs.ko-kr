---
title: 데이터 최적화를 위한 성능 튜닝
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a8143bae69e85ecf0056dcb9433707a681a69077
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271888"
---
# <a name="performance-for-r-services---data-optimization"></a>R Services에 대 한 성능-데이터 최적화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 두 사례 연구를 기반으로 R 서비스에 대 한 성능 최적화를 설명 하는 시리즈의 세 번째입니다. 이 문서에서는 SQL Server에서 실행 되는 R 또는 Python 스크립트의 성능 최적화에 대해 설명 합니다. 또한 성능을 향상 시키고 알려진 문제를 방지 하기 위해 R 코드를 업데이트 하는 데 사용할 수 있는 방법도 설명 합니다.

## <a name="choosing-a-compute-context"></a>계산 컨텍스트 선택

SQL Server 2016 및 2017에서 R 또는 Python 스크립트를 실행할 때 **로컬** 또는 **SQL** 계산 컨텍스트를 사용할 수 있습니다.

**로컬** 계산 컨텍스트를 사용 하는 경우 분석은 서버가 아닌 컴퓨터에서 수행 됩니다. 따라서 코드에서 사용할 SQL Server 데이터를 가져오는 경우 네트워크를 통해 데이터를 인출 해야 합니다. 이 네트워크 전송으로 인해 발생하는 성능 저하는 전송된 데이터 크기, 네트워크 속도 및 동시에 발생하는 다른 네트워크 전송에 따라 달라집니다.

**SQL Server 계산 컨텍스트**를 사용 하는 경우 코드는 서버에서 실행 됩니다. SQL Server에서 데이터를 가져오는 경우 분석을 실행 하는 서버에 대 한 로컬 데이터 여야 하므로 네트워크 오버 헤드가 발생 하지 않습니다. 다른 원본에서 데이터를 가져와야 하는 경우 ETL을 미리 정렬 하는 것이 좋습니다.

큰 데이터 집합을 사용할 경우 항상 SQL 컴퓨팅 컨텍스트를 사용하세요.

## <a name="factors"></a>요소

R 언어에는 범주 데이터에 대 한 특수 변수인 *요소*개념이 있습니다. 데이터 과학자는 범주 변수를 요소로 처리 하는 것이 기계 학습 함수에 의해 올바르게 처리 되도록 하기 때문에 수식에서 요소 변수를 사용 하는 경우가 많습니다. 자세한 내용은 Dummies에 대 [한 R을 참조 하세요. 요소 변수](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

디자인에 따라 요소 변수를 문자열에서 정수로 변환 하 고 저장 또는 처리를 위해 다시 되돌릴 수 있습니다. 인수 stringsAsFactors `data.frame` 가 **False**로 설정 되어 있지 않으면 R 함수는 모든 문자열을 요소 변수로 처리 합니다. 즉, 문자열은 처리를 위해 정수로 자동 변환 된 다음 원래 문자열로 다시 매핑됩니다.

요소에 대 한 원본 데이터를 정수로 저장 하는 경우 R은 런타임에 계수 정수를 문자열로 변환 하 고 자체 내부 문자열에서 정수로 변환을 수행 하기 때문에 성능이 저하 될 수 있습니다.

이러한 런타임 변환을 방지 하려면 값을 SQL Server 테이블에 정수로 저장 하 고 _colInfo_ 인수를 사용 하 여 인수로 사용 되는 열의 수준을 지정 하는 것이 좋습니다. RevoScaleR의 대부분의 데이터 원본 개체는 _colInfo_매개 변수를 사용 합니다. 이 매개 변수를 사용 하 여 데이터 원본에서 사용 하는 변수의 이름을 지정 하 고, 해당 유형을 지정 하 고, 열 값에 대 한 변수 수준 또는 변환을 정의 합니다.

예를 들어 다음 R 함수 호출은 테이블에서 정수 1, 2, 3을 가져오지만 "apple", "주황색" 및 "바나나" 수준이 있는 요소에 값을 매핑합니다.

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

원본 열에 문자열이 포함 된 경우 _colInfo_ 매개 변수를 사용 하 여 미리 수준을 미리 지정 하는 것이 항상 더 효율적입니다. 예를 들어 다음 R 코드는 문자열을 읽는 동안 요소로 처리 합니다.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

모델 생성에 의미 체계 차이가 없으면 후자의 방법으로 인해 성능이 향상 될 수 있습니다.

## <a name="data-transformations"></a>데이터 변환

데이터 과학자는 대개 분석의 일부로 R로 작성된 변환 함수를 사용합니다. 변환 함수는 테이블에서 검색 된 각 행에 적용 됩니다. SQL Server에서 이러한 변환은 일괄 처리에서 검색 된 모든 행에 적용 되며,이는 R 인터프리터와 분석 엔진 간의 통신이 필요 합니다. 변환을 수행하기 위해 데이터는 SQL에서 분석 엔진을 이동하고 나서 R 인터프리터 프로세스로 이동하고 그 반대로 이동합니다.

따라서 R 코드의 일부로 변환을 사용 하면 관련 된 데이터 양에 따라 알고리즘의 성능에 큰 영향을 미칠 수 있습니다.

분석을 수행 하기 전에 테이블이 나 뷰에 필요한 모든 열을 포함 하 고 계산 중에 변환을 방지 하는 것이 더 효율적입니다. 기존 테이블에 다른 열을 추가할 수 없는 경우 변환된 열이 포함된 다른 테이블 또는 뷰를 만들고 적절한 쿼리를 사용하여 데이터를 검색하는 것이 좋습니다.

## <a name="batch-row-reads"></a>일괄 처리 행 읽기

코드에 SQL Server 데이터 소스 (`RxSqlServerData`)를 사용 하는 경우 _rowsperread_ 매개 변수를 사용 하 여 일괄 처리 크기를 지정 하는 것이 좋습니다. 이 매개 변수는 쿼리 되 고 처리를 위해 외부 스크립트로 전송 되는 행 수를 정의 합니다. 런타임에 알고리즘은 각 일괄 처리에서 지정 된 개수의 행만 볼 수 있습니다.

한 번에 처리 되는 데이터 양을 제어 하는 기능을 통해 문제를 해결 하거나 문제를 방지할 수 있습니다. 예를 들어 입력 데이터 집합이 매우 광범위 하거나 (열이 많은 경우) 데이터 집합에 몇 개의 큰 열 (예: 자유 텍스트)이 있는 경우 메모리에서 페이징 데이터를 방지 하기 위해 일괄 처리 크기를 줄일 수 있습니다.

기본적으로 메모리가 부족 한 컴퓨터 에서도 성능을 보장 하기 위해이 매개 변수의 값은 5만로 설정 됩니다. 서버에 사용 가능한 메모리가 충분 한 경우이 값을 50만로 늘리거나 백만 개를 초과 하 여 더 나은 성능을 얻을 수 있습니다. 특히 규모가 작은 테이블의 경우에는 더욱 그렇습니다.

일괄 처리 크기를 늘릴 경우의 이점은 큰 데이터 집합 및 여러 프로세스에서 실행 될 수 있는 작업에서 명백 하 게 됩니다. 그러나이 값을 늘려도 항상 최상의 결과를 얻을 수 있는 것은 아닙니다. 최적의 값을 결정 하기 위해 데이터 및 알고리즘을 시험해 보는 것이 좋습니다.

## <a name="parallel-processing"></a>병렬 처리

**Rx** 분석 함수의 성능을 향상 시키려면 SQL Server 기능을 활용 하 여 서버 컴퓨터에서 사용 가능한 코어를 사용 하 여 작업을 병렬로 실행할 수 있습니다.

SQL Server에서 R을 사용 하 여 병렬화 하는 방법에는 두 가지가 있습니다.

-   **병렬 \@을 사용 합니다.** `sp_execute_external_script` 저장 프로시저를 사용하여 R 스크립트를 실행할 경우 `@parallel` 매개 변수를 `1`로 설정합니다. R 스크립트에서 처리를 위한 다른 메커니즘을 사용 하는 RevoScaleR 함수를 사용 **하지** 않는 경우에 가장 적합 한 방법입니다. 스크립트가 RevoScaleR 함수 (일반적으로 "rx"로 시작)를 사용 하는 경우 병렬 처리는 자동으로 수행 되며를 명시적으로로 `@parallel` `1`설정할 필요가 없습니다.

    R 스크립트를 병렬화 할 수 있고 SQL 쿼리를 병렬화 할 수 있는 경우 데이터베이스 엔진은 여러 병렬 프로세스를 만듭니다. 만들 수 있는 최대 프로세스 수는 인스턴스의 최대 **병렬 처리 수준** (MAXDOP) 설정과 같습니다. 그러면 모든 프로세스가 동일한 스크립트를 실행 하지만 데이터의 일부만 수신 합니다.
    
    따라서이 방법은 모델을 학습 하는 경우와 같이 모든 데이터를 확인 해야 하는 스크립트에는 유용 하지 않습니다. 하지만 병렬로 일괄 처리 예측과 같은 태스크를 수행할 경우 이 방법이 유용합니다. 에서 병렬 처리 `sp_execute_external_script`를 사용 하는 방법에 대 한 자세한 내용은 [transact-sql에서 R 코드 사용](../tutorials/quickstart-r-create-script.md)의 **고급 팁: 병렬 처리** 섹션을 참조 하세요.

-   **NumTasks = 1을 사용 합니다.** SQL Server 계산 컨텍스트에서 **rx** 함수를 사용 하는 경우 _numtasks_ 매개 변수의 값을 만들려는 프로세스 수로 설정 합니다. 만든 프로세스 수는 **MAXDOP**보다 많을 수 없습니다. 그러나 생성 되는 실제 프로세스 수는 데이터베이스 엔진에 의해 결정 되며, 요청 된 수보다 적을 수 있습니다.

    R 스크립트를 병렬화 할 수 있고 SQL 쿼리를 병렬화 할 수 있는 경우 SQL Server은 rx 함수를 실행할 때 여러 병렬 프로세스를 만듭니다. 실제로 생성 되는 프로세스의 수는 리소스 관리, 현재 리소스 사용량, 기타 세션 및 R 스크립트와 함께 사용 되는 쿼리에 대 한 쿼리 실행 계획 등의 다양 한 요소에 따라 다릅니다.

## <a name="query-parallelization"></a>쿼리 병렬 처리

Microsoft R에서는 데이터를 RxSqlServerData 데이터 원본 개체로 정의 하 여 SQL Server 데이터 원본으로 작업할 수 있습니다.

전체 테이블 또는 뷰를 기반으로 데이터 원본을 만듭니다.

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

SQL 쿼리를 기반으로 데이터 원본을 만듭니다.

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 테이블이 쿼리 대신 데이터 원본에 지정 된 경우 R Services는 내부 추론을 사용 하 여 테이블에서 인출할 필수 열을 결정 합니다. 그러나이 방법은 병렬 실행이 될 가능성이 낮습니다.

데이터를 병렬로 분석할 수 있도록 하기 위해 데이터를 검색 하는 데 사용 되는 쿼리는 데이터베이스 엔진이 병렬 쿼리 계획을 만들 수 있는 방법으로 사용 해야 합니다. 코드 또는 알고리즘이 대용량 데이터를 사용 하는 경우에 `RxSqlServerData` 제공 된 쿼리가 병렬 실행을 위해 최적화 되어 있는지 확인 합니다. 병렬 실행 계획을 생성하지 않는 쿼리에서는 계산에 대한 단일 프로세스가 생성될 수 있습니다.

대량 데이터 집합으로 작업 해야 하는 경우 R 코드를 실행 하기 전에 Management Studio 또는 다른 SQL 쿼리 분석기를 사용 하 여 실행 계획을 분석 합니다. 그런 다음 권장 단계를 수행 하 여 쿼리 성능을 향상 시킵니다. 예를 들어 테이블에 대한 누락된 인덱스가 쿼리 실행에 걸리는 시간에 영향을 미칠 수 있습니다. 자세한 내용은 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)을 참조 하세요.

성능에 영향을 줄 수 있는 또 다른 일반적인 실수는 쿼리가 필요한 것 보다 많은 열을 검색 하는 것입니다. 예를 들어 수식이 3 개의 열만 기반으로 하지만 원본 테이블에 30 개의 열이 있는 경우 데이터를 불필요 하 게 이동 하는 것입니다.

 + 사용 `SELECT *`하지 마십시오.
 + 일정 시간 내에 데이터 집합의 열을 검토 하 고 분석에 필요한 항목만 식별
 + GUID 및 rowguids와 같은 R 코드와 호환 되지 않는 데이터 형식이 포함 된 열을 쿼리에서 제거 합니다.
 + 지원 되지 않는 날짜 및 시간 형식 확인
 + 테이블을 로드 하는 대신 특정 값을 선택 하거나 열을 캐스팅 하 여 변환 오류를 방지 하는 뷰를 만듭니다.

## <a name="optimizing-the-machine-learning-algorithm"></a>기계 학습 알고리즘 최적화

이 섹션에서는 Microsoft R의 RevoScaleR 및 기타 옵션과 관련 된 기타 팁과 리소스를 제공 합니다.

> [!TIP]
> R 최적화에 대 한 일반적인 설명은이 문서의 범위를 벗어나는 것입니다. 그러나 코드를 더 신속 하 게 만들어야 하는 경우에는 자주 사용 하 [는 문서인 R](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)인 문서를 사용 하는 것이 좋습니다. 이 샘플은 R의 프로그래밍 구문과 선명한 언어 및 세부 정보에 대 한 일반적인 문제를 다루며, R 프로그래밍 기술에 대 한 다양 한 특정 예제를 제공 합니다.

### <a name="optimizations-for-revoscaler"></a>RevoScaleR에 대 한 최적화

많은 RevoScaleR 알고리즘은 학습 된 모델을 생성 하는 방법을 제어 하는 매개 변수를 지원 합니다. 모델의 정확성과 정확성은 중요 하지만 알고리즘의 성능은 중요할 수 있습니다. 정확도와 학습 시간 사이에 적절 한 균형을 유지 하기 위해 매개 변수를 수정 하 여 계산 속도를 높일 수 있으며, 대부분의 경우 정확도 나 정확성을 줄이지 않고 성능을 향상 시킬 수 있습니다.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`의사 결정 트리의 깊이를 제어 하는 매개변수를지원합니다.`maxDepth` 이 `maxDepth` 증가 함에 따라 성능이 저하 될 수 있으므로 깊이와 저하 성능을 높이는 이점을 분석 하는 것이 중요 합니다.

    `maxNumBins` `maxDepth`,, 및`maxSurrogate`와 같은 매개 변수를 조정하여시간복잡성과예측정확도간의균형을제어할수도있습니다.`maxComplete` 깊이를 10 또는 15 이상으로 늘리면 계산에 비용이 매우 많이 들 수 있습니다.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    수식의 첫 번째 `cube` 종속 변수가 요소 변수인 경우 인수를 사용해 보세요.
    
    가 `cube` 로`TRUE`설정 되 면 회귀는 분할 된 역을 사용 하 여 수행 됩니다 .이는 표준 회귀 계산 보다 더 빠르고 메모리를 사용할 수 있습니다. 수식에 많은 변수가 있으면 성능이 상당히 향상될 수 있습니다.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    첫 번째 `cube` 종속 변수가 요소 변수인 경우 인수를 사용 합니다.
    
    가 `cube` 로`TRUE`설정 된 경우 알고리즘은 분할 된 역을 사용 하며,이는 더 빠르고 메모리를 더 사용할 수 있습니다. 수식에 많은 변수가 있으면 성능이 상당히 향상될 수 있습니다.

RevoScaleR 최적화에 대 한 추가 지침은 다음 문서를 참조 하세요.

+ 지원 문서: [RxDForest 및 rxDTree에 대 한 성능 조정 옵션](https://support.microsoft.com/kb/3104235)

+ 모델을 제어 하기 위한 메서드는 승격 된 트리 모델에 맞게 조정 됩니다. [추계 그라데이션 부스트를 사용 하 여 모델 예측](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ RevoScaleR에서 데이터를 이동 및 처리 하는 방법에 대 한 개요: [ScaleR에서 사용자 지정 청크 알고리즘 작성](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR 용 프로그래밍 모델: [RevoScaleR에서 스레드 관리](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ [RxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest) 에 대 한 함수 참조

+ [RxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees) 에 대 한 함수 참조

### <a name="use-microsoftml"></a>MicrosoftML 사용

또한 RevoScaleR에서 제공 하는 계산 컨텍스트 및 변환을 사용할 수 있는 확장 가능한 기계 학습 알고리즘을 제공 하는 새로운 **MicrosoftML** 패키지를 살펴보는 것이 좋습니다.

+ [MicrosoftML 시작](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [MicrosoftML 알고리즘을 선택 하는 방법](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Microsoft R Server를 사용 하 여 솔루션 운영

저장 된 모델을 사용 하 여 빠른 예측을 수행 하거나 기계 학습을 응용 프로그램에 통합 하는 시나리오의 경우 Microsoft R Server의 [운영 화](https://docs.microsoft.com/r-server/what-is-operationalization) 기능 (이전의 deployr)을 사용할 수 있습니다.

+ **데이터 과학자**, [mrsdeploy 패키지](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) 를 사용 하 여 r 코드를 다른 컴퓨터와 공유 하 고, 웹, 데스크톱, 모바일 및 대시보드 응용 프로그램 내에서 r analytics를 통합 합니다. [R Server에서 R 웹 서비스를 게시 및 관리 하는 방법](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ **관리자**는 패키지를 관리 하 고, 웹 노드 및 계산 노드를 모니터링 하 고, R 작업에 대 한 보안을 제어 하는 방법에 대해 알아봅니다. [R에서 웹 서비스와 상호 작용 하 고 사용 하는 방법](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>이 시리즈의 문서

[R에 대 한 성능 조정-소개](sql-server-r-services-performance-tuning.md)

[R SQL Server 구성에 대 한 성능 조정](sql-server-configuration-r-services.md)

[R의 성능 튜닝-R 코드 및 데이터 최적화](r-and-data-optimization-r-services.md)

[성능 튜닝-사례 연구 결과](performance-case-study-r-services.md)
