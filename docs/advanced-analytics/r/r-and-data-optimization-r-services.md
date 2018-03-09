---
title: "R Services-데이터 최적화에 대 한 성능 | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0ca7a57b10787ca183c2979fe95a5e3fe446dc86
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="performance-for-r-services---data-optimization"></a>R Services-데이터 최적화에 대 한 성능
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 두 사례 연구를 기반으로 하는 R 서비스에 대 한 성능 최적화를 설명 하는 일련의 세 번째입니다. 이 문서에서는 성능 최적화 R에 대 한 설명 또는 SQL Server에서 실행 하는 Python 스크립트입니다. 또한 성능을 향상 시키기 및 알려진된 문제를 방지 하기 위해 R 코드를 업데이트 하는 데 사용할 수 있는 방법을 설명 합니다.

## <a name="choosing-a-compute-context"></a>계산 컨텍스트를 선택합니다.

SQL Server 2016 및 2017에서 사용할 수 있습니다는 **로컬** 또는 **SQL** Python 또는 R 스크립트를 실행할 때 컨텍스트를 계산 합니다.

사용 하는 경우는 **로컬** 사용자 컴퓨터와 서버에 없는 분석 계산 컨텍스트에서 수행 됩니다. 따라서 코드에서 사용 하도록 SQL Server에서 데이터를 가져오는 경우 데이터는 네트워크를 통해 가져온 해야 합니다. 이 네트워크 전송으로 인해 발생하는 성능 저하는 전송된 데이터 크기, 네트워크 속도 및 동시에 발생하는 다른 네트워크 전송에 따라 달라집니다.

사용 하는 경우는 **SQL Server 계산 컨텍스트**, 코드가 서버에서 실행 됩니다. SQL Server에서 데이터를 가져오는 경우 데이터 분석을 실행 하는 서버에 로컬 며 따라서 네트워크 오버 헤드 없음 도입 되었습니다. 다른 원본에서 데이터를 가져올 해야 할 경우에 ETL를 미리 정렬 하는 것이 좋습니다.

큰 데이터 집합을 사용할 경우 항상 SQL 계산 컨텍스트를 사용하세요.

## <a name="factors"></a>요소

R 언어에는 범주 데이터에 대 한 특별 한 변수는 "요소" 개념이 있습니다. 데이터 과학자 often의 수식에 인수 변수를 사용, 데이터 확인 요소로 범주 변수를 처리 하기 때문에 컴퓨터 학습 함수로 올바르게 처리 됩니다. 자세한 내용은 참조 하십시오. [for Dummies R: 비율 변수] (http://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

기본적으로 정수 및 저장소 또는 처리를 위해 다시 백 비율 변수 문자열에서 변환할 수 있습니다. R `data.frame` 하지 않는 한 함수 인수 변수로 모든 문자열을 처리 인수 *stringsAsFactors* 로 설정 된 **False**합니다. 따라서 처리를 위해 정수로 변환 되 고 원래 문자열에 다시 매핑될 다음 문자열은 자동으로.

요소에 대 한 원본 데이터를 정수로 저장 되 면 R 런타임 시 비율 정수가을 문자열로 변환 하 고 다음 자체 내부 문자열을 정수로 변환 수행 하기 때문에 성능이 떨어질 수 있습니다.

이러한 런타임 변환을 방지 하려면 SQL Server 테이블에 정수로 값을 저장 하 고 사용 하 여 고려는 _colInfo_ 인수를 인수로 사용 되는 열에 대 한 수준을 지정 합니다. 매개 변수를 사용 하는 대부분의 데이터 원본 개체에서 RevoScaleR _colInfo_합니다. 이 매개 변수를 사용 하 여 데이터 원본에 의해 사용 되는 변수 이름을 지정 하 고의 형식에를 지정한 열 값에 대해 변수 수준 또는 변환을 정의 합니다.

예를 들어 다음 R 함수 호출은 1, 2 및 3 정수 테이블에서 가져오지만 "apple" 수준으로 요소를 값, "주황색" 및 "바나나"에 매핑합니다.

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

원본 열에서 문자열을 포함 된 경우는 것이 항상 더 효율적으로 사용 하 여 미리 수준을 지정할 수는 _colInfo_ 매개 변수입니다. 예를 들어 다음 R 코드를 읽고 되 고에 문자열 요소를 처리 합니다.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

모델 생성의 의미 체계 차이점이 이면 후자의 방법을 사용할 경우 성능이 향상 될 수 있습니다.

## <a name="data-transformations"></a>데이터 변환

데이터 과학자는 대개 분석의 일부로 R로 작성된 변환 함수를 사용합니다. 변환 함수는 테이블에서 검색 된 각 행에 적용 됩니다. SQL Server에서 이러한 변환은 R 인터프리터와 분석 엔진 간에 통신 해야 하는 일괄 처리에서 검색 된 모든 행에 적용 됩니다. 변환을 수행하기 위해 데이터는 SQL에서 분석 엔진을 이동하고 나서 R 인터프리터 프로세스로 이동하고 그 반대로 이동합니다.

이러한 이유로 변환을 사용 하 여 R 코드의 일부로 관련 된 데이터의 양에 따라 알고리즘의 성능에 상당한 부정적인 영향을 개뿐입니다.

테이블 또는 뷰의 분석을 수행 하기 전에 필요한 모든 열이 있어야 하 고 계산 하는 동안 변환 방지를 더 효율적입니다. 기존 테이블에 다른 열을 추가할 수 없는 경우 변환된 열이 포함된 다른 테이블 또는 뷰를 만들고 적절한 쿼리를 사용하여 데이터를 검색하는 것이 좋습니다.

## <a name="batch-row-reads"></a>일괄 처리 행 읽기

SQL Server 데이터 소스를 사용 하는 경우 (`RxSqlServerData`) 코드의 매개 변수를 사용 하 여 시도 하는 권장 _rowsPerRead_ 일괄 처리 크기를 지정 합니다. 이 매개 변수 쿼리하고 처리에 대 한 외부 스크립트를 전송 하는 행의 수를 정의 합니다. 런타임 시 알고리즘은 지정된 된 수의 각 일괄 처리의 행을 볼 수 있습니다.

한 번에 처리 하는 데이터 양을 제어 하는 기능 해결 하거나 문제를 방지할 수 있습니다. 예를 들어, 입력된 데이터 집합이 매우 넓은 경우 (많은 열에) 또는 데이터 집합에 적은 수의 큰 열 (예: 일반 텍스트), 데이터를 페이징 메모리 부족을 방지 하기 위해 일괄 처리 크기를 줄일 수 있습니다.

기본적으로 메모리 부족으로 좋은 성능을 보장 하기 위해이 매개 변수 값을 50000 설정 됩니다. 서버에 충분 한 사용 가능한 메모리에 있는 경우 500, 000 또는 백만이 값을 늘리면 특히 큰 테이블에 대 한 더 나은 성능을 얻을 수 있습니다.

일괄 처리 크기를 늘리면의 이점을 여러 프로세스에서 실행할 수 있는 작업 및 큰 데이터 집합에 분명 하 게 됩니다. 그러나이 값을 늘리면지 않습니다 하지 항상 최상의 결과 제공 합니다. 데이터와 가장 적합 한 값을 결정 하는 알고리즘으로 실험 하는 것이 좋습니다.

## <a name="parallel-processing"></a>병렬 처리

성능을 향상 시키기 위해 **rx** 분석 함수 사용 가능한 코어를 사용 하 여 서버 컴퓨터에 병렬로 작업을 실행 하는 SQL Server의 기능을 활용할 수 있습니다.

SQL Server에서 R로 병렬화를 달성 하기 위해 두 가지가 있습니다.

-   **사용 하 여 \@병렬 합니다.** `sp_execute_external_script` 저장 프로시저를 사용하여 R 스크립트를 실행할 경우 `@parallel` 매개 변수를 `1`로 설정합니다. R 스크립트는 경우이 최상의 방법을 **하지** 처리를 위해 다른 메커니즘을 포함 하는 RevoScaleR 함수를 사용 합니다. 스크립트 RevoScaleR 함수 (일반적으로 "rx" 접두사로 있음)를 사용 하 여 병렬 처리는 자동으로 수행 하 고 명시적으로 설정할 필요가 없습니다 `@parallel` 를 `1`합니다.

    R 스크립트를 평행 화할 수 및 SQL 쿼리를 병렬화 할 경우 데이터베이스 엔진에서는 여러 병렬 프로세스 만듭니다. 만들 수 있는 프로세스의 최대는 같은 **x degree of** 인스턴스에 대 한 (MAXDOP) 설정 합니다. 모든 프로세스는 다음 동일한 스크립트를 실행 하지만 데이터의 일부만 수신 합니다.
    
    이 메서드는 예를 들어 모든 데이터를 표시 해야 하는 스크립트와 유용 따라서 모델을 학습 합니다. 하지만 병렬로 일괄 처리 예측과 같은 태스크를 수행할 경우 이 방법이 유용합니다. 병렬 처리를 사용 하 여 대 한 자세한 내용은 `sp_execute_external_script`, 참조는 **팁 고급: 병렬 처리** 섹션 [TRANSACT-SQL에서 R 코드를 사용 하 여](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)합니다.

-   **NumTasks를 사용 하 여 = 1입니다.** 사용 하는 경우 **rx** 의 값을 설정 하는 SQL Server 계산 컨텍스트에서 함수는 _numTasks_ 매개 변수를 만들려고 할 프로세스의 수입니다. 만든 프로세스 수가 될 수 없습니다 이상 **MAXDOP**; 그러나 생성 프로세스의 실제 수는 데이터베이스 엔진에 의해 결정 됩니다 및 보다 작은 요청할 수 있습니다.

    R 스크립트를 평행 화할 수 및 SQL 쿼리를 병렬화 할 경우 SQL Server에서는 rx 함수를 실행할 때 여러 병렬 프로세스 만듭니다. 만든 프로세스의 실제 수는 다양 한 리소스 관리 등의 요소, 리소스, 다른 세션 및 R 스크립트와 함께 사용 하는 쿼리에 대 한 쿼리 실행 계획의 현재 사용량에 따라 다릅니다.

## <a name="query-parallelization"></a>쿼리 병렬화

Microsoft R에서 RxSqlServerData 데이터 원본 개체와 데이터를 정의 하 여 SQL Server 데이터 원본 작업할 수 있습니다.

전체 테이블 또는 뷰를 기반으로 하는 데이터 소스를 만듭니다.

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

SQL 쿼리를 기반으로 데이터 원본을 만듭니다.

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 테이블을 쿼리 하는 대신 데이터 원본에 지정 R 서비스를 사용 하 여 내부 추론 필요한 열이 테이블에서 인출할 수를 결정 합니다. 그러나이 방법은 병렬 실행 될 가능성이 있으므로있지 않습니다.

을 보장 하기 위해 동시에 데이터를 분석할 수 있습니다 데이터를 검색 하는 데 사용 하는 쿼리는 데이터베이스 엔진에는 병렬 쿼리 계획을 만들 수 있도록 하는 방식으로 묶을 수 해야 합니다. 코드 또는 알고리즘에서 많은 양의 데이터를 사용 하는 경우에 지정 된 쿼리 `RxSqlServerData` 병렬 실행을 위해 최적화 됩니다. 병렬 실행 계획을 생성하지 않는 쿼리에서는 계산에 대한 단일 프로세스가 생성될 수 있습니다.

큰 데이터 집합을 사용 해야 할 경우 실행 계획을 분석 하려면 Management Studio 또는 R 코드를 실행 하기 전에 다른 SQL 쿼리 분석기를 사용 합니다. 그런 다음 쿼리 성능을 향상 시키기 위해 권장된 단계를 수행할 수 있습니다. 예를 들어 테이블에 대한 누락된 인덱스가 쿼리 실행에 걸리는 시간에 영향을 미칠 수 있습니다. 자세한 내용은 참조 [모니터링 및 성능 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)합니다.

성능에 영향을 줄 수 있는 또 다른 일반적인 실수는 쿼리가 필요한 것 보다 더 많은 열을 검색 하는 합니다. 예를 들어 수식 세 개의 열을 기반으로 하지만 원본 테이블에 열이 30, 이동 하는 경우 데이터 불필요 하 게 합니다.

 + 사용 하지 않도록 `SELECT *`!
 + 데이터 집합의 열을 검토 하 고 분석에 필요한 개체만 식별 하는 데 시간이 걸릴
 + GUID 및 rowguids 등의 R 코드와 호환 되지 않는 데이터 형식이 포함 된 열 쿼리에서 제거
 + 지원 되지 않는 날짜 및 시간 형식에 대 한 확인
 + 테이블을 로드 하지 않고 특정 값을 선택 하거나 변환 오류를 방지 하려면 열을 캐스팅 하는 보기 만들기

## <a name="optimizing-the-machine-learning-algorithm"></a>기계 학습 알고리즘을 최적화합니다.

이 섹션에서는 기타 팁과 RevoScaleR 및 Microsoft R에서 다른 옵션에 관련 된 리소스

> [!TIP]
> R 최적화에 대 한 일반적인 설명은이 문서의 범위를 벗어났습니다. 그러나 코드를 더 빠르게 확인 해야 하는 경우 권장 인기 있는 문서 [The R 르노](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf)합니다. R에서 프로그래밍 구문과 선명한 언어 및 자세한 정보에 대 한 일반적인 문제에 설명 하 고 프로그래밍 기술 하는 R의 여러 특정 예제를 제공 합니다.

### <a name="optimizations-for-revoscaler"></a>RevoScaleR에 대 한 최적화

많은 RevoScaleR 알고리즘에 매개 변수는 학습 된 모델 생성 방법을 제어를 지원 합니다. 정확도 및 모델의 정확성을 중요 한 알고리즘의 성능을 만큼 중요 한 역할 수 있습니다. 정확도 및 학습 시간 사이의 올바른 균형을 가져오려면 더 빠른 속도의 계산 및 대부분의 경우에서, 정확성 나 저하 없이 성능을 향상 하는 매개 변수를 수정할 수 있습니다.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`지원 된 `maxDepth` 매개 변수는 의사 결정 트리의 깊이 제어 합니다. 로 `maxDepth` 은 증가 하면 성능이 저하 될 수 있습니다, 성능을 저하 시키는 비교 깊이가 증가의 혜택을 분석 하는 것이 중요 되기 때문입니다.

    와 같은 매개 변수를 조정 하 여 시간 복잡성 및 예측 정확도 간의 균형을 제어할 수 있습니다 `maxNumBins`, `maxDepth`, `maxComplete`, 및 `maxSurrogate`합니다. 깊이를 10 또는 15 이상으로 늘리면 계산에 비용이 매우 많이 들 수 있습니다.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    사용 하 여 시도 `cube` 인수 경우 수식에서 첫 번째 종속 변수는 변수입니다.
    
    때 `cube` 로 설정 된 `TRUE`, 회귀 속도가 더 빠를 수 및 표준 회귀 계산 보다 적은 메모리를 사용할 수 있는 분할 된 역함수 값을 사용 하 여 수행 됩니다. 수식에 많은 변수가 있으면 성능이 상당히 향상될 수 있습니다.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    사용 하 여는 `cube` 첫 번째 종속 변수가 변수 인수입니다.
    
    때 `cube` 로 설정 된 `TRUE`, 알고리즘에서 속도가 더 빠를 수 있습니다 및 메모리를 적게 사용 하는 분할 된 역함수 값을 사용 합니다. 수식에 많은 변수가 있으면 성능이 상당히 향상될 수 있습니다.

RevoScaleR의 최적화에서 추가 지침은 다음이 문서를 참조 합니다.

+ 지원 문서: [성능 튜닝 rxDForest 및 rxDTree에 대 한 옵션](https://support.microsoft.com/kb/3104235)

+ 승격된 된 트리 모델에 맞게 모델을 제어 하는 방법: [예측 모델 사용 하 여 추측 경사](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ RevoScaleR 이동 하 고 데이터를 처리 하는 방법을 간략하게: [ScaleR에서 사용자 지정 청크 알고리즘 작성](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR에 대 한 프로그래밍 모델: [RevoScaleR의 스레드 관리](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ 함수에 대 한 참조 [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ 함수에 대 한 참조 [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Use MicrosoftML

또한 좋습니다 새 보면 **MicrosoftML** 계산 컨텍스트 및 RevoScaleR에서 제공 하는 변환에 사용할 수 있는 확장 가능한 기계 학습 알고리즘을 제공 하는 패키지입니다.

+ [MicrosoftML 시작](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [MicrosoftML 알고리즘을 선택 하는 방법](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Microsoft R Server를 사용 하는 솔루션 운영 화

사용자 시나리오에서는 저장 된 모델을 사용 하 여 빠른 예측 하거나 기계 학습 응용 프로그램 통합을 사용할 수 있습니다 하는 경우는 [해결해줍니다](https://docs.microsoft.com/r-server/what-is-operationalization) Microsoft R Server (이전의 DeployR)의 기능입니다.

+ 로 **데이터 과학자**를 사용 하 여는 [mrsdeploy 패키지](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) 하 R 코드를 다른 컴퓨터와 공유 하 고 웹, 데스크톱, 모바일, 및 대시보드 응용 프로그램 분석 R 통합: [게시 하는 방법 R 서버에서 R 웹 서비스를 관리 하 고](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ 로 **관리자**, 패키지 관리, 웹 노드를 모니터링 하는 방법은 계산 노드, 및 R 작업에 대 한 보안 제어: [상호 작용 하며 R에서 웹 서비스를 사용 하는 방법](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>이 시리즈의 기사

[성능-R에 대 한 튜닝 소개](sql-server-r-services-performance-tuning.md)

[R-SQL Server 구성에 대 한 성능 조정](sql-server-configuration-r-services.md)

[R-R에 대 한 성능 조정 코드 및 데이터 최적화](r-and-data-optimization-r-services.md)

[성능 튜닝-사례 연구 결과](performance-case-study-r-services.md)
