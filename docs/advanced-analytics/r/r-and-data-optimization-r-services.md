---
title: SQL Server Machine Learning Services-데이터 최적화를 위한 성능 튜닝
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b6e25ec0c7bc1ce332514910cdaf5cdf9fdb9e07
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432406"
---
# <a name="performance-for-r-services---data-optimization"></a>R Services-데이터 최적화에 대 한 성능
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 두 가지 사용 사례에 따라 R Services에 대 한 성능 최적화를 설명 하는 일련의 세 번째입니다. 이 문서에서는 R에 대 한 성능 최적화를 설명 또는 SQL Server에서 실행 되는 Python 스크립트입니다. 알려진된 문제를 방지 하 고 성능을 향상 시키기 위해 R 코드를 업데이트 하는 데 사용할 수 있는 방법을 설명 합니다.

## <a name="choosing-a-compute-context"></a>계산 컨텍스트를 선택합니다.

SQL Server 2016 및 2017에서는 사용할 수 있습니다 합니다 **로컬** 하거나 **SQL** 계산 컨텍스트에서 R 또는 Python 스크립트를 실행 하는 경우.

사용 하는 경우는 **로컬** 계산 컨텍스트를 분석 하 고 서버에 없는 컴퓨터에 수행 됩니다. 따라서 코드에서 사용 하도록 SQL Server에서 데이터를 가져오는 경우 네트워크를 통해 데이터를 가져올 수 있어야 합니다. 이 네트워크 전송으로 인해 발생하는 성능 저하는 전송된 데이터 크기, 네트워크 속도 및 동시에 발생하는 다른 네트워크 전송에 따라 달라집니다.

사용 하는 경우는 **SQL Server 계산 컨텍스트에서**, 코드가 서버에서 실행 됩니다. SQL 서버에서 데이터를 가져오고 데이터 분석을 실행 하는 서버에 로컬 이어야 합니다 하 고 따라서 네트워크 오버 헤드 없이 도입 되었습니다. 다른 원본에서 데이터를 가져오는 경우에 ETL를 미리 정렬 하는 것이 좋습니다.

큰 데이터 집합을 사용할 경우 항상 SQL 계산 컨텍스트를 사용하세요.

## <a name="factors"></a>요소

R 언어에 대 한 개념이 *요인*는 범주 데이터에 대 한 특수 변수입니다. 데이터 과학자는 종종 수식에서 요소 변수를 사용, 범주 변수 요소로 처리 되도록 데이터 때문에 machine learning 함수에서 제대로 처리 됩니다. 자세한 내용은 참조 하세요. [for Dummies R: 요소 변수](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)합니다.

기본적으로 정수를 저장 또는 처리를 위해 다시 백 요소 변수 문자열에서 변환할 수 있습니다. R `data.frame` 하지 않으면 함수 요소 변수도 모든 문자열을 처리 인수 *stringsAsFactors* 로 설정 되어 **False**합니다. 즉, 처리에 대 한 정수로 변환 되 고 원래 문자열에 다시 매핑됩니다 다음 문자열은 자동으로 합니다.

요소에 대 한 원본 데이터는 정수로 저장 되 면 R 런타임에 문자열을 비율 정수를 변환 하 고 자체 내부 문자열을 정수로 변환 수행 하기 때문에 성능이 떨어질 수 있습니다.

이러한 런타임 변환을 방지 하려면 SQL Server 테이블에 정수로 값을 저장 하 고 사용 하는 것이 좋습니다 합니다 _colInfo_ 요소로 사용 된 열에 대 한 수준을 지정 하는 인수입니다. RevoScaleR의 대부분의 데이터 원본 개체에는 매개 변수 사용 _colInfo_합니다. 데이터 원본에서 사용 하는 변수 이름, 형식 지정, 열 값에 변수 수준 또는 변환 정의를이 매개 변수를 사용 합니다.

예를 들어, 다음 R 함수 호출은 1, 2 및 3의 정수 테이블에서 가져오지만 "banana", "주황색" 및 "apple" 수준 사용 하 여 요소를 값에 매핑합니다.

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

문자열에 포함 되어 있으면 원본 열이이 항상 좀 더 효율적으로 사용 하 여 미리 수준을 지정 합니다 _colInfo_ 매개 변수입니다. 예를 들어, 다음 R 코드를 읽을 때 처럼에 문자열을 요소로 처리 합니다.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

모델 생성에의 미적인 차이가 없으면 있으면 후자의 방법을 더 나은 성능을 발생할 수 있습니다.

## <a name="data-transformations"></a>데이터 변환

데이터 과학자는 대개 분석의 일부로 R로 작성된 변환 함수를 사용합니다. 변환 함수는 테이블에서 검색 된 각 행에 적용 됩니다. SQL Server에서 이러한 변환은 R 인터프리터와 분석 엔진 간의 통신 해야 하는 일괄 처리에서 검색 된 모든 행에 적용 됩니다. 변환을 수행하기 위해 데이터는 SQL에서 분석 엔진을 이동하고 나서 R 인터프리터 프로세스로 이동하고 그 반대로 이동합니다.

따라서이 변환을 사용 하 여 R 코드의 일부로 관련 된 데이터의 양에 따라 알고리즘의 성능에 매우 부정적인 영향을 있습니다.

이 테이블 또는 뷰의 분석을 수행 하기 전에 필요한 모든 열이 있어야 하 고 계산 하는 동안 변환을 방지 하기 위해 더 효율적입니다. 기존 테이블에 다른 열을 추가할 수 없는 경우 변환된 열이 포함된 다른 테이블 또는 뷰를 만들고 적절한 쿼리를 사용하여 데이터를 검색하는 것이 좋습니다.

## <a name="batch-row-reads"></a>일괄 처리 행 읽기

SQL Server 데이터 원본을 사용 하는 경우 (`RxSqlServerData`) 코드에서 매개 변수를 사용을 시도 하는 권장 _rowsPerRead_ 일괄 처리 크기를 지정 합니다. 이 매개 변수는 쿼리 및 처리에 대 한 외부 스크립트에 전송 되는 행 수를 정의 합니다. 런타임에 알고리즘에 지정 된 각 일괄 처리의 행 수가 표시 됩니다.

한 번에 처리 되는 데이터의 양을 제어 하는 기능 해결 하거나 문제를 방지할 수 있습니다. 예를 들어 입력된 데이터 집합이 매우 되었습니다 (열 수 있음) 또는 데이터 집합에 적은 수의 큰 열 (예: 일반 텍스트) 하는 경우 메모리 부족 데이터를 페이징 하지 않으려면 일괄 처리 크기를 줄일 수 있습니다.

기본적으로이 매개 변수의 메모리를 사용 하 여 컴퓨터에도 훌륭한 성능을 보장 하기 위해, 50000으로 설정 됩니다. 서버에 사용 가능한 메모리가 부족할 경우을 500,000 또는 백만도이 값을 늘리면 특히 큰 테이블에 대 한 더 나은 성능을 얻을 수 있습니다.

일괄 처리 크기를 증가 시키는 이점 여러 프로세스에서 실행할 수 있는 작업에 큰 데이터 집합에 대해 분명 하 게 됩니다. 그러나이 값을 늘리면 생성 하지 않습니다 항상 최상의 결과. 데이터 및 최적 값을 결정 하는 알고리즘을 사용 하 여 실험 하는 것이 좋습니다.

## <a name="parallel-processing"></a>병렬 처리

성능을 향상 시키려면 **rx** 분석 함수 사용 가능한 코어를 사용 하 여 서버 컴퓨터에 병렬로 작업을 실행 하는 SQL Server의 기능을 활용할 수 있습니다.

두 가지 방법으로 SQL Server에서 R 사용 하 여 병렬 처리를 위해 수 있습니다.

-   **사용 하 여 \@병렬입니다.** `sp_execute_external_script` 저장 프로시저를 사용하여 R 스크립트를 실행할 경우 `@parallel` 매개 변수를 `1`로 설정합니다. R 스크립트는 경우이 최상의 방법을 **되지** 처리를 위한 다른 메커니즘을 포함 하는 RevoScaleR 함수를 사용 합니다. 스크립트에서 RevoScaleR 함수 (일반적으로 "rx" 접두사로 있음), 병렬 처리는 자동으로 수행 하 고 명시적으로 설정할 필요가 없습니다 `@parallel` 에 `1`입니다.

    R 스크립트를 병렬 처리할 수 하는 경우와 SQL 쿼리를 병렬 처리할 수 있으면 데이터베이스 엔진이 여러 병렬 프로세스를 만듭니다. 만들 수 있는 프로세스의 최대 수는 같음 합니다 **최대 병렬 처리 수준** 인스턴스에 대 한 (MAXDOP) 설정 합니다. 모든 프로세스는 다음 동일한 스크립트를 실행 하지만 데이터의 일부만 수신 합니다.
    
    따라서이 메서드는 때와 같이 모든 데이터를 확인 해야 하는 스크립트를 사용 하 여 유용 하지는 모델을 학습 합니다. 하지만 병렬로 일괄 처리 예측과 같은 태스크를 수행할 경우 이 방법이 유용합니다. 병렬 처리를 사용 하 여 대 한 자세한 내용은 `sp_execute_external_script`를 참조 합니다 **고급 팁: 병렬 처리** 의 섹션 [TRANSACT-SQL에서 R 코드를 사용 하 여](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)합니다.

-   **NumTasks 사용 = 1입니다.** 사용 하는 경우 **rx** 함수를 SQL Server 계산 컨텍스트에서 값을 설정 합니다 _numTasks_ 매개 변수를 만들려면 하려는 프로세스의 수입니다. 그러나 생성 된 프로세스 수가 수 없습니다 둘 **MAXDOP**생성 된 프로세스의 실제 수는 데이터베이스 엔진에 의해 결정 됩니다 하 고 보다 작은지를 요청할 수 있습니다.

    R 스크립트를 병렬 처리할 수 있고 SQL 쿼리를 병렬 처리할 수 있는 경우, 다음 SQL Server에서는 여러 병렬 프로세스 rx 함수를 실행 하는 경우 생성 된 프로세스의 실제 수는 다양 한 리소스 거 버 넌 스와 같은 요소, 리소스, 기타 세션 및 R 스크립트를 사용 하 여 사용 하는 쿼리의 쿼리 실행 계획의 현재 사용량에 따라 달라 집니다.

## <a name="query-parallelization"></a>쿼리 병렬 처리

Microsoft R에서 RxSqlServerData 데이터 원본 개체와 데이터를 정의 하 여 SQL Server 데이터 원본을 사용 하 여 작업할 수 있습니다.

전체 테이블 또는 뷰를 기반으로 하는 데이터 소스를 만듭니다.

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

SQL 쿼리를 기반으로 데이터 원본을 만듭니다.

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> R Services 내부 추론을 사용 하 여 테이블에서 페치할 필요한 열을 결정 하는 테이블을 쿼리 하는 대신 데이터 원본에 지정 된 경우 그러나이 방법은 병렬 실행 가능성이 아닙니다.

을 보장 하기 위해 병렬로 데이터를 분석할 수 있습니다 이러한 방식으로 데이터베이스 엔진은 병렬 쿼리 계획을 만들 수 데이터를 검색 하는 쿼리를 표현 되어야 합니다. 코드 또는 알고리즘에서 많은 양의 데이터를 사용 하는 경우 확인에 제공 된 쿼리 `RxSqlServerData` 병렬 실행을 위해 최적화 됩니다. 병렬 실행 계획을 생성하지 않는 쿼리에서는 계산에 대한 단일 프로세스가 생성될 수 있습니다.

큰 데이터 집합을 사용 하는 경우 실행 계획을 분석 하려면 Management Studio 또는 R 코드를 실행 하기 전에 다른 SQL 쿼리 분석기를 사용 합니다. 그런 다음 쿼리의 성능 향상을 위해 모든 권장 되는 단계를 수행 합니다. 예를 들어 테이블에 대한 누락된 인덱스가 쿼리 실행에 걸리는 시간에 영향을 미칠 수 있습니다. 자세한 내용은 [모니터링 및 성능 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)합니다.

성능에 영향을 줄 수 있는 또 다른 일반적인 실수는 쿼리가 필요한 것 보다 더 많은 열을 검색 하는입니다. 예를 들어 수식 세 개의 열을 기반으로 하지만 원본 테이블에 열이 30을 이동 하는 경우 데이터 불필요 하 게 합니다.

 + 사용 하지 않도록 `SELECT *`!
 + 데이터 집합의 열을 검토 하 고 분석을 위해 필요한 것만을 식별 하는 데 시간이 소요
 + GUID rowguids 등 R 코드를 사용 하 여 호환 되지 않는 데이터 형식이 포함 된 열을 쿼리에서 제거
 + 지원 되지 않는 날짜 및 시간 형식에 대 한 확인
 + 테이블을 로드 하지 않고 특정 값을 선택 하거나 변환 오류를 방지 하려면 열을 캐스팅 하는 보기 만들기

## <a name="optimizing-the-machine-learning-algorithm"></a>기계 학습 알고리즘을 최적화

이 섹션에서는 기타 팁 및 RevoScaleR 및 Microsoft R에서 다른 옵션에 관련 된 리소스를 제공 합니다.

> [!TIP]
> R 최적화에 대 한 일반적인 설명은이 문서의 범위를 벗어났습니다. 그러나 코드를 더 빠르게 확인 하는 경우 좋습니다 인기 있는 문서를 [The R 지옥](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)합니다. R에서 프로그래밍 구문 및 선명한 언어 및 세부 정보에서 일반적인 문제에 설명 하 고 많은 R 프로그래밍 방법의 예를 제공 합니다.

### <a name="optimizations-for-revoscaler"></a>RevoScaleR에 대 한 최적화

대부분의 RevoScaleR 알고리즘 학습된 된 모델 생성 방법을 제어 하는 매개 변수를 지원 합니다. 모델의 정밀도 정확도 중요 하지만, 알고리즘의 성능이 동일 하 게 중요 한 수 있습니다. 정확도 및 학습 시간 간에 적절 한 균형을 얻으려면 대부분의 경우에 계산의 속도 높이고, 나 정확도 줄이지 않고 성능을 개선할 매개 변수를 수정할 수 있습니다.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` 지원 된 `maxDepth` 의사 결정 트리의 깊이 제어 하는 매개 변수입니다. 으로 `maxDepth` 는 증가 성능 저하 될 수 있습니다, 되므로 성능 저하 및 깊이 증가 시키는 이점 분석 하는 것이 중요 합니다.

    와 같은 매개 변수를 조정 하 여 시간 복잡성과 예측 정확도 간의 균형을 제어할 수도 있습니다 `maxNumBins`, `maxDepth`를 `maxComplete`, 및 `maxSurrogate`합니다. 깊이를 10 또는 15 이상으로 늘리면 계산에 비용이 매우 많이 들 수 있습니다.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    사용 하 여 시도 `cube` 수식에서 첫 번째 종속 변수가 요소 변수가 경우 인수입니다.
    
    때 `cube` 로 설정 된 `TRUE`, 회귀 더 빠를 수 및 표준 회귀 계산 보다 적은 메모리를 사용할 수 있는 분할된 된 역함수를 사용 하 여 수행 됩니다. 수식에 많은 변수가 있으면 성능이 상당히 향상될 수 있습니다.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    사용 된 `cube` 첫 번째 종속 변수가 요소 변수일 경우 인수입니다.
    
    때 `cube` 로 설정 된 `TRUE`, 알고리즘은 분할된 된 역함수 더 빠를 수 고 적은 메모리를 사용할 수 있습니다. 수식에 많은 변수가 있으면 성능이 상당히 향상될 수 있습니다.

RevoScaleR의 최적화에 대 한 추가 지침, 이러한 문서를 참조 하세요.

+ 문서를 지원 합니다. [성능 튜닝 rxDForest 및 rxDTree에 대 한 옵션](https://support.microsoft.com/kb/3104235)

+ 향상 된 트리 모델에 맞게 모델을 제어 하기 위한 메서드: [예측 확률 그라데이션 부스 팅을 사용 하 여 모델](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ RevoScaleR의 이동 및 데이터를 처리 하는 방법의 개요: [ScaleR의 사용자 지정 청크 알고리즘 작성](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR에 대 한 프로그래밍 모델: [RevoScaleR의 스레드 관리](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ 함수에 대 한 참조 [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ 함수에 대 한 참조 [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>MicrosoftML 사용

새를 확인 하는 것이 좋습니다 **MicrosoftML** RevoScaleR에서 제공 하는 변환을 확인 하 고 계산 컨텍스트를 사용할 수 있는 확장 가능한 기계 학습 알고리즘을 제공 하는 패키지입니다.

+ [MicrosoftML 시작](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [MicrosoftML 알고리즘을 선택 하는 방법](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Microsoft R Server를 사용 하는 솔루션을 운영 화

시나리오에는 저장 된 모델을 사용 하 여 빠른 예측이 포함 또는 기계 학습 응용 프로그램 통합을 사용할 수 있습니다 하는 경우는 [운영 화](https://docs.microsoft.com/r-server/what-is-operationalization) Microsoft R Server (이전의 DeployR)의 기능입니다.

+ 로 **데이터 과학자**를 사용 합니다 [mrsdeploy 패키지](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) 다른 컴퓨터를 사용 하 여 R 코드를 공유 하 고 웹, 데스크톱, 모바일 및 대시보드 응용 프로그램 내에서 R 분석을 통합 하: [게시 및 R Server에서 R 웹 서비스를 관리 하는 방법](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ 로 **관리자**, 패키지 관리, 웹 노드를 모니터링 하는 방법 및 계산 노드 및 R 작업에 대 한 보안 제어 합니다. [R services와 상호 작용 및 웹을 사용 하는 방법](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>이 시리즈의 기사

[성능 튜닝-R에 대 한 소개](sql-server-r-services-performance-tuning.md)

[R-SQL Server 구성에 대 한 성능 조정](sql-server-configuration-r-services.md)

[R-R의 성능 튜닝 코드 및 데이터 최적화](r-and-data-optimization-r-services.md)

[성능 튜닝-사례 연구 결과](performance-case-study-r-services.md)
