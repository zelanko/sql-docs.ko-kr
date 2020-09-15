---
title: 데이터 성능 조정
description: 이 문서에서는 SQL Server에서 실행할 R 또는 Python 스크립트의 성능 최적화에 관해 설명합니다. 또한 성능을 개선하고 알려진 문제를 방지하기 위해 R 코드를 업데이트하는 데 사용할 수 있는 방법을 설명합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/15/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 95600d85c02d120f1bb4df2e7a73411a9965550a
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179999"
---
# <a name="performance-for-r-services---data-optimization"></a>R Services 성능 - 데이터 최적화
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이 문서는 두 가지 사례 연구를 기준으로 R Services를 위한 성능 최적화를 설명하는 시리즈의 세 번째 문서입니다. 이 문서에서는 SQL Server에서 실행할 R 또는 Python 스크립트의 성능 최적화에 관해 설명합니다. 또한 성능을 개선하고 알려진 문제를 방지하기 위해 R 코드를 업데이트하는 데 사용할 수 있는 방법을 설명합니다.

## <a name="choosing-a-compute-context"></a>컴퓨팅 컨텍스트 선택

SQL Server 2016 및 2017에서 R 또는 Python 스크립트를 실행할 때 **로컬** 또는 **SQL** 컴퓨팅 컨텍스트를 사용할 수 있습니다.

**로컬** 컴퓨팅 컨텍스트를 사용하는 경우 분석은 서버가 아닌 컴퓨터에서 수행됩니다. 따라서 코드에서 사용할 SQL Server 데이터를 가져오는 경우 네트워크를 통해 데이터를 가져와야 합니다. 이 네트워크 전송으로 인해 발생하는 성능 저하는 전송된 데이터 크기, 네트워크 속도 및 동시에 발생하는 다른 네트워크 전송에 따라 달라집니다.

**SQL Server 컴퓨팅 컨텍스트**를 사용하는 경우 코드는 서버에서 실행됩니다. SQL Server에서 데이터를 가져오는 경우 데이터는 분석을 실행하는 서버에 있어야 하므로 네트워크 오버헤드가 발생하지 않습니다. 다른 원본에서 데이터를 가져와야 하는 경우 ETL을 미리 처리하는 것이 좋습니다.

큰 데이터 집합을 사용할 경우 항상 SQL 컴퓨팅 컨텍스트를 사용하세요.

## <a name="factors"></a>요소

R 언어에는 범주 데이터의 특수 변수인 ‘요소’ 개념이 있습니다.  데이터 과학자는 수식에서 요소 변수를 사용하는 경우가 많은데, 이는 범주 변수를 요소로 처리하면 기계 학습 함수에서 데이터가 제대로 처리되기 때문입니다. 자세한 내용은 [R for Dummies: Factor Variables](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)(더미에 대한 R: 요소 변수)를 참조하세요.

저장이나 처리를 위해 의도적으로 요소 변수를 문자열에서 정수로 변환하거나 다시 그 반대로 변환할 수 있습니다. *stringsAsFactors* 인수가 **False**로 설정된 경우가 아니면 R `data.frame` 함수는 모든 문자열을 요소 변수로 처리합니다. 즉, 문자열은 처리를 위해 자동으로 정수로 변환된 후 다시 원래 문자열에 매핑됩니다.

R은 런타임에 요소 정수를 문자열로 변환한 후 자체 내부 문자열에서 정수로 변환을 수행하기 때문에 요소의 원본 데이터가 정수로 저장되면 성능이 저하될 수 있습니다.

이 런타임 변환을 방지하려면 값을 SQL Server 테이블에 정수로 저장하고 _colInfo_ 인수를 사용하여 요소로 사용되는 열의 수준을 지정하는 것이 좋습니다. RevoScaleR의 대부분 데이터 원본 개체는 매개 변수 _colInfo_를 사용합니다. 이 매개 변수를 사용하여 데이터 원본에서 사용하는 변수의 이름을 지정하고, 해당 형식을 지정하고, 열 값에 대한 변수 수준 또는 변환을 정의합니다.

예를 들어 다음 R 함수 호출은 테이블에서 정수 1, 2 및 3을 가져오지만 “apple”, “orange” 및 “banana” 수준을 사용하여 값을 요소에 매핑합니다.

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

원본 열에 문자열이 포함된 경우 _colInfo_ 매개 변수를 사용하여 미리 수준을 미리 지정하는 것이 더 효율적입니다. 예를 들어 다음 R 코드는 문자열을 읽을 때 요소로 처리합니다.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

모델 생성에 의미 체계 차이점이 없다면 나중 방법으로 성능을 개선할 수 있습니다.

## <a name="data-transformations"></a>데이터 변환

데이터 과학자는 대개 분석의 일부로 R로 작성된 변환 함수를 사용합니다. 변환 함수는 테이블에서 검색된 각 행에 적용됩니다. SQL Server에서 이 변환은 일괄 처리로 검색된 모든 행에 적용되며, 이 변환에는 R 인터프리터와 분석 엔진 간 통신이 필요합니다. 변환을 수행하기 위해 데이터는 SQL에서 분석 엔진을 이동하고 나서 R 인터프리터 프로세스로 이동하고 그 반대로 이동합니다.

이런 이유로 변환을 R 코드의 일부로 사용할 경우 포함된 데이터 양에 따라 알고리즘 성능에 매우 부정적인 영향을 미칠 수 있습니다.

분석을 수행하기 전에 테이블 및 뷰에 모든 필요한 열을 포함하고 계산 중에 변환을 방지하는 것이 더 효율적입니다. 기존 테이블에 다른 열을 추가할 수 없는 경우 변환된 열이 포함된 다른 테이블 또는 뷰를 만들고 적절한 쿼리를 사용하여 데이터를 검색하는 것이 좋습니다.

## <a name="batch-row-reads"></a>일괄 처리 행 읽기

코드에서 SQL Server 데이터 원본(`RxSqlServerData`)을 사용하는 경우 _rowsPerRead_ 매개 변수를 사용하여 일괄 처리 크기를 지정하는 것이 좋습니다. 이 매개 변수는 쿼리된 후 처리를 위해 외부 스크립트로 전송되는 행 수를 정의합니다. 런타임에 알고리즘은 각 일괄 처리에서 지정된 개수의 행만 확인합니다.

한 번에 처리되는 데이터 양을 제어하는 기능을 통해 문제를 해결하거나 방지할 수 있습니다. 예를 들어 입력 데이터 세트가 매우 광범위하거나(많은 열 포함) 데이터 세트에 몇 개의 큰 열(예: 일반 텍스트)이 있는 경우 페이징 데이터로 인해 메모리 부족 현상이 일어나지 않도록 일괄 처리 크기를 줄일 수 있습니다.

메모리가 부족한 머신에서도 괜찮은 성능을 보장하도록 기본적으로 이 매개 변수 값은 50000으로 설정됩니다. 서버에 사용 가능한 메모리가 충분히 있는 경우 이 값을 500,000 또는 1,000,000으로 늘리면 특히 큰 테이블의 경우 성능이 향상될 수 있습니다.

일괄 처리 크기를 늘릴 경우의 이점은 큰 데이터 세트 및 여러 프로세스에서 실행될 수 있는 작업에서 더 분명히 나타납니다. 그러나 이 값을 늘려도 항상 최상의 결과를 얻을 수 있는 것은 아닙니다. 데이터 및 알고리즘을 실험하여 최적 값을 결정하는 것이 좋습니다.

## <a name="parallel-processing"></a>병렬 처리

**rx** 분석 함수의 성능을 개선하기 위해 SQL Server 기능을 활용하여 서버 컴퓨터에서 사용 가능한 코어를 사용하여 작업을 병렬로 실행할 수 있습니다.

SQL Server에서 R을 통해 병렬 처리를 수행하려면 다음 두 가지 방법을 사용합니다.

-   **\@parallel을 사용합니다.** `sp_execute_external_script` 저장 프로시저를 사용하여 R 스크립트를 실행할 경우 `@parallel` 매개 변수를 `1`로 설정합니다. 이 방법은 R 스크립트에서 다른 처리 메커니즘을 포함하는 RevoScaleR 함수를 사용하지 **않는** 경우 가장 적합합니다. 스크립트가 RevoScaleR 함수(일반적으로 “rx”가 접두사로 추가됨)를 사용하는 경우 병렬 처리는 자동으로 수행되며 `@parallel`을 `1`로 명시적으로 설정할 필요가 없습니다.

    R 스크립트를 병렬 처리할 수 있으며 SQL 쿼리를 병렬 처리할 수 있는 경우 데이터베이스 엔진은 여러 병렬 프로세스를 만듭니다. 만들 수 있는 최대 프로세스 수는 인스턴스의 MAXDOP(**최대 병렬 처리 수준**) 설정과 같습니다. 모든 프로세스는 동일한 스크립트를 실행하지만 데이터의 일부만 수신합니다.
    
    따라서 모델을 학습하는 경우와 같이 모든 데이터를 확인해야 하는 스크립트에서는 이 방법이 유용하지 않습니다. 하지만 병렬로 일괄 처리 예측과 같은 태스크를 수행할 경우 이 방법이 유용합니다. `sp_execute_external_script`를 통해 병렬 처리를 사용하는 방법에 대한 자세한 내용은 [Transact-SQL에서 R 코드 사용](../tutorials/quickstart-r-create-script.md)의 **고급 팁: 병렬 처리** 섹션을 참조하세요.

-   **numTasks =1을 사용합니다.** SQL Server 컴퓨팅 컨텍스트에서 **rx** 함수를 사용하는 경우 _numTasks_ 매개 변수의 값을 만들려는 프로세스 수로 설정합니다. 생성되는 프로세스 수는 **MAXDOP**보다 클 수 없지만, 생성되는 실제 프로세스 수는 데이터베이스 엔진에서 결정되며 요청한 것보다 적을 수 있습니다.

    R 스크립트를 병렬 처리할 수 있고 SQL 쿼리를 병렬 처리할 수 있는 경우 SQL Server에서는 rx 함수를 실행할 때 여러 병렬 프로세스를 만듭니다. 생성되는 실제 프로세스 수는 리소스 관리, 현재 리소스 사용량, 기타 세션, R 스크립트에서 사용되는 쿼리의 쿼리 실행 계획과 같은 다양한 요소에 따라 달라집니다.

## <a name="query-parallelization"></a>쿼리 병렬 처리

Microsoft R에서 데이터를 RxSqlServerData 데이터 원본 개체로 정의하여 SQL Server 데이터 원본을 사용할 수 있습니다.

전체 테이블 또는 뷰를 기반으로 데이터 원본을 만듭니다.

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

SQL 쿼리를 기반으로 데이터 원본을 만듭니다.

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 테이블이 쿼리가 아닌 데이터 원본에서 지정된 경우 R Services는 내부 휴리스틱을 사용하여 테이블에서 가져올 필요한 열을 결정하지만 이 방법으로는 병렬 실행이 이루어지지 않을 수 있습니다.

데이터를 병렬로 분석할 수 있게 하려면 데이터 검색에 사용되는 쿼리가 데이터베이스 엔진이 병렬 쿼리 계획을 만들 수 있는 방식으로 표현되어야 합니다. 코드 또는 알고리즘이 대용량 데이터를 사용하는 경우 `RxSqlServerData`에 제공된 쿼리가 병렬 실행에 최적화되어 있는지 확인합니다. 병렬 실행 계획을 생성하지 않는 쿼리에서는 계산에 대한 단일 프로세스가 생성될 수 있습니다.

큰 데이터 세트를 사용해야 하는 경우 R 코드를 실행하기 전에 Management Studio 또는 다른 SQL 쿼리 분석기를 사용하여 실행 계획을 분석합니다. 그런 다음, 권장 단계를 수행하여 쿼리 성능을 개선합니다. 예를 들어 테이블에 대한 누락된 인덱스가 쿼리 실행에 걸리는 시간에 영향을 미칠 수 있습니다. 자세한 내용은 [성능 모니터링 및 조정](../../relational-databases/performance/monitor-and-tune-for-performance.md)을 참조하세요.

성능에 영향을 줄 수 있는 또 다른 일반적인 실수는 쿼리가 필요한 것보다 많은 열을 검색하는 것입니다. 예를 들어 수식에 3개 열만 사용되지만, 원본 테이블에 30개 열이 있는 경우에는 데이터를 불필요하게 이동하는 것입니다.

 + `SELECT *`를 사용하지 마세요.
 + 시간을 내어 데이터 세트의 열을 검토하고 분석에 필요한 열만 식별
 + GUID 및 rowguid와 같이 R 코드와 호환되지 않는 데이터 형식이 포함된 열을 쿼리에서 제거
 + 지원되지 않는 날짜 및 시간 형식 확인
 + 테이블을 로드하는 대신 특정 값을 선택하거나 열을 캐스팅하여 변환 오류를 방지하는 뷰 만들기

## <a name="optimizing-the-machine-learning-algorithm"></a>기계 학습 알고리즘 최적화

이 섹션에서는 Microsoft R의 RevoScaleR 및 기타 옵션에 관련된 기타 팁과 리소스를 제공합니다.

> [!TIP]
> R 최적화에 대해서는 이 문서에서 설명하지 않습니다. 그러나 코드를 더 빠르게 만들어야 하는 경우에는 인기 있는 [R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf) 문서를 추천합니다. 이 문서에서는 R의 프로그래밍 구문과 생생한 언어와 세부 정보의 일반적인 단점을 다루며, R 프로그래밍 기술의 구체적인 많은 예제를 제공합니다.

### <a name="optimizations-for-revoscaler"></a>RevoScaleR 최적화

많은 RevoScaleR 학습 알고리즘은 학습 모델 생성 방법을 제어하는 매개 변수를 지원합니다. 모델의 정밀도와 정확도가 중요하지만, 알고리즘 성능도 똑같이 중요할 수 있습니다. 정확도와 학습 시간 사이에 적절한 균형을 맞추기 위해 계산 속도를 높이고 대부분의 경우 정밀도나 정확도를 줄이지 않고 성능을 개선하도록 매개 변수를 수정할 수 있습니다.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`는 의사 결정 트리 수준을 제어하는 `maxDepth` 매개 변수를 지원합니다. `maxDepth`가 증가하면 성능이 저하될 수 있으므로 수준 증가 및 성능 저하 시 이점을 분석해야 합니다.

    `maxNumBins`, `maxDepth`, `maxComplete` 및 `maxSurrogate`와 같은 매개 변수를 조정하여 시간 복잡성과 예측 정확도 간에 균형을 제어할 수도 있습니다. 깊이를 10 또는 15 이상으로 늘리면 계산에 비용이 매우 많이 들 수 있습니다.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    수식의 첫 번째 종속 변수가 요소 변수인 경우 `cube` 인수를 사용하세요.
    
    `cube`가 `TRUE`로 설정되면 분할된 역함수를 사용하여 회귀가 수행되고 표준 회귀 계산보다 더 빠르고 더 적은 메모리를 사용할 수 있습니다. 수식에 많은 변수가 있으면 성능이 상당히 향상될 수 있습니다.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    첫 번째 종속 변수가 요소 변수인 경우 `cube` 인수를 사용합니다.
    
    `cube`가 `TRUE`로 설정되면 알고리즘은 분할된 역함수를 사용하며 더 빠르고 더 적은 메모리를 사용할 수 있습니다. 수식에 많은 변수가 있으면 성능이 상당히 향상될 수 있습니다.

RevoScaleR 최적화에 대한 추가 지침은 다음 문서를 참조하세요.

+ 지원 문서: [Performance Tuning Options for rxDForest and rxDTree](https://support.microsoft.com/kb/3104235)(rxDForest 및 rxDTree에 대한 성능 조정 옵션)

+ 모델 제어 방법이 승격된 트리 모델에 맞게 조정됩니다. [Estimating Models Using Stochastic Gradient Boosting](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)(예측 모델이 확률적 경사 부스팅을 사용하고 있음)

+ RevoScaleR이 데이터를 이동 및 처리하는 방법에 대한 개요: [Write custom chunking algorithms in ScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)(ScaleR에서 사용자 지정 청크 알고리즘 작성)

+ RevoScaleR용 프로그래밍 모델: [Managing threads in RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)(RevoScaleR에서 스레드 관리)

+ [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)에 대한 함수 참조

+ [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)에 대한 함수 참조

### <a name="use-microsoftml"></a>MicrosoftML 사용

RevoScaleR에서 제공하는 컴퓨팅 컨텍스트 및 변환을 사용할 수 있는 확장성 있는 기계 학습 알고리즘을 제공하는 새로운 **MicrosoftML** 패키지를 살펴보는 것이 좋습니다.

+ [Get started with MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)(MicrosoftML 시작)

+ [How to choose a MicrosoftML algorithm](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)(MicrosoftML 알고리즘을 선택하는 방법)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Microsoft R Server를 사용하여 솔루션 운영화

시나리오에서 저장된 모델을 사용하거나 기계 학습을 애플리케이션에 통합하여 빠른 예측을 수행하는 경우 Microsoft R Server (이전 DeployR)에서 [운영화](https://docs.microsoft.com/r-server/what-is-operationalization) 기능을 사용할 수 있습니다.

+ **데이터 과학자**로 [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) 패키지를 사용하여 R 코드를 다른 컴퓨터와 공유하고 R 분석을 웹, 데스크톱, 모바일 및 대시보드 애플리케이션 내부에 통합할 수 있습니다. [How to publish and manage R web services in R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)(R Server에서 R 웹 서비스를 게시 및 관리하는 방법)

+ **관리자**로 패키지를 관리하고, 웹 노드 및 컴퓨팅 노드를 모니터링하고, R 작업의 보안을 제어하는 방법을 알아봅니다. [How to interact with and consume web services in R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)(R에서 웹 서비스와 상호 작용하고 웹 서비스를 사용하는 방법)

## <a name="articles-in-this-series"></a>이 시리즈의 문서

[R의 성능 튜닝 - 소개](sql-server-r-services-performance-tuning.md)

[R의 성능 조정 - SQL Server 구성](sql-server-configuration-r-services.md)

[R의 성능 조정 - R 코드 및 데이터 최적화](r-and-data-optimization-r-services.md)

[성능 조정 - 사례 연구 결과](performance-case-study-r-services.md)
