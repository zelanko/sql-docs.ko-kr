---
title: "R 및 데이터 최적화 (R 서비스) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# R 및 데이터 최적화 (R 서비스)
이 항목에서는 성능을 개선 하거나 알려진된 문제를 방지 하기에 R 코드를 업데이트 하기 위한 메서드를 설명 합니다.

## 컨텍스트를 계산 합니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 하나를 사용할 수는 __로컬__ 또는 __SQL__ 분석을 수행할 때 컨텍스트를 계산 합니다. 사용 하는 경우는 __로컬__ 계산 컨텍스트를 분석 클라이언트 컴퓨터에서 수행 되 고 데이터에서 가져와야 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 네트워크를 통해 합니다. 성능 저하가 네트워크 전송을 전송 하 고, 데이터는 네트워크의 속도의 크기에 따라 결정 및 다른 네트워크 전송에 발생 하는 동시에 발생 합니다.

계산 컨텍스트가 __SQL Server__, 분석 함수는 내부에서 실행 한 후 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 데이터 분석 작업에 로컬 이므로 네트워크 오버 헤드가 없음 정의 되었습니다. 

큰 데이터 집합으로 작업할 때는 항상 SQL 계산 컨텍스트를 사용 해야 합니다.

## 요소

R 언어 요소를 테이블에서 문자열을 변환합니다. 여러 데이터 원본 개체 걸릴 `colInfo` 열이 처리 되는 방법을 제어 하는 매개 변수로 합니다. 예를 들어 `c(“fruit” = c(type = “factor”, levels=as.character(c(1:3)), newLevels=c(“apple”, “orange”, “banana”)))` 정수 1, 2 및 3 테이블에서 사용 되며 요소 수준으로 동일 하 게 취급 `apple`, `orange`, 및 `banana`합니다. 

데이터 과학자의 수식;에 자주 요소 변수를 사용 그러나 원본 데이터는 정수 하는 경우에 요소를 사용 하 여 발생 하므로 성능 런타임에 정수를 문자열로 변환 합니다. 그러나 문자열 열에 포함 하는 경우 사용 하 여 동시 미리 수준을 지정할 수 `colInfo`합니다. 이 경우에 해당 하는 문을 수는  `c(“fruit” = c(type = “factor”, levels= c(“apple”, “orange”, “banana”)))`, 를 읽으면 되 고 요인으로 문자열을 처리 합니다. 

실행된 시간 변환을 방지 하려면 테이블에 정수 수준을 저장 하 고 첫 번째 수식 예에 설명 된 대로를 사용해 것이 좋습니다. 모델 생성의 의미 체계 차이가 있으면이 방법을 더 나은 성능을 발생할 수 있습니다.

## 데이터 변환

데이터 과학자는 종종 R 분석의 일환으로 작성 된 변환 함수를 사용 합니다. 변환 함수는 테이블에서 검색 된 각 행에 적용 되어야 합니다.  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 이 변환을 일괄 처리 모드에서 발생 하 고 R 인터프리터 및 분석 엔진 간의 통신을 포함 합니다. 분석 엔진 이동한 다음 R 인터프리터 프로세스 및 백 SQL에서 데이터 이동 하 여 변환을 수행 합니다. 따라서 변환 수에서는 상당한에 부정적인 영향이 알고리즘의 성능을 사용 하 여 데이터의 양에 따라 참여 합니다.

테이블 또는 뷰의 분석을 수행 하기 전에 필요한 모든 열이 계산 중 변환을 방지 하도록 더 효율적입니다. 기존 테이블에 추가 열을 추가할 수 없는 경우 변환 된 열이 있는 다른 테이블 또는 뷰를 만드는 것이 좋습니다 하 고 적절 한 쿼리를 사용 하 여 데이터를 검색 합니다.

## 일괄 처리

SQL 데이터 원본 (`RxSqlServerData`)에 매개 변수를 사용 하는 일괄 처리 크기를 지정 하는 옵션이 `rowsPerRead`합니다. 이 매개 변수는 한 번에 처리할 행 수를 지정 합니다. 런타임 시 알고리즘을 지정 된 각 일괄 처리의 행 번호가 표시 됩니다. 기본적으로이 매개 변수 값 설정은 50, 000 개를 알고리즘은 메모리 부족으로 컴퓨터에도 잘 수행할 수 있는지 확인 합니다. 컴퓨터에 충분 한 사용 가능한 메모리를 500, 000 또는 심지어 100만이 값을 늘리면 특히 큰 테이블에 더 나은 성능을 얻을 수 있습니다. 

이 값을 늘리면 더 나은 결과 생성 하지 않을 수 있습니다 및 가장 적합 한 값을 확인 하려면 몇 가지 실험에 필요할 수 있습니다. 이 혜택은 여러 프로세스와 큰 데이터 집합에 더 확인할 수 있습니다 (`numTasks` 보다 큰 값으로 설정 `1`).

## 병렬 처리

Rx 내부 분석 함수 실행의 성능을 향상 시키기 위해 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 사용 가능한 코어를 사용 하 여 병렬 처리에 의존는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터입니다. 사용한 병렬 처리를 수행 하는 방법은 두 가지가 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]:

* 사용 하는 경우는 `sp_execute_external_script` 설정 하는 R 스크립트를 실행 하려면 저장된 프로시저는 `@parallel` 매개 변수를 `1`합니다. 일반적으로 "rx" 접두사가 붙은 RevoScaleR 함수를 사용 하지 않는 R 스크립트에 유용 합니다. 스크립트 RevoScaleR 함수를 사용 하 여 병렬 처리는 자동으로 처리 하 고 설정 하지 않아야 하는 경우 `@parallel` 를 `1`합니다.

    R 스크립트를 평행 화할 수, 경우에 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 쿼리 평행 화할 수, 다음 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 여러 병렬 프로세스를 만듭니다 (최대는 __최대 병렬 처리 수준 MAXDOP__ 에 대 한 설정 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)],) 모든 프로세스에서 동일한 스크립트를 실행 합니다. 각 프로세스 수신 된 데이터의 일부 이므로 이것이 같은 모든 데이터를 참조 해야 하는 스크립트를 통해 유용한 모델을 학습할 때입니다. 그러나는 경우에 유용 병렬로 일괄 처리 예측 등의 작업을 수행 합니다. 병렬 처리를 사용 하 여 대 한 자세한 내용은 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), 참조는 __고급 팁: 병렬 처리__ 섹션 [TRANSACT-SQL에서 R 코드를 사용 하 여](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)합니다.

* Rx 함수는 SQL Server 계산 컨텍스트를 사용할 때는 `numTasks` 만들려는 프로세스의 수입니다. 생성 된 프로세스의 실제 수에 의해 결정 됩니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 요청한 것 보다 작을 수 있습니다. 생성 된 프로세스 수가 수 없는 이상 __MAXDOP__합니다.

    R 스크립트를 평행 화할 수, 경우에 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 쿼리 평행 화할 수, 다음 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] rx 함수를 실행 하는 경우 여러 병렬 프로세스를 만듭니다.

만들어질 수 있는 프로세스의 다양 한 리소스 관리와 같은 요소, 리소스, 다른 세션 및 R 스크립트와 함께 사용 하는 쿼리에 대 한 쿼리 실행 계획의 현재 사용량에 따라 다릅니다. 

### 쿼리 병렬화

을 보장 하기 위해 동시에 데이터를 분석할 수 있습니다 데이터를 검색 하는 데 사용 하는 쿼리를 렌더링할 수 자체에 대해 병렬 실행 하는 방식으로 묶을 수 해야 합니다. 

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 사용 하 여 SQL 데이터 원본을 사용한 작업을 지원 `RxSqlServerData` 소스를 지정 합니다. 원본은 테이블 또는 쿼리를 수 있습니다. 예를 들어 다음 코드 예제 모두 SQL 쿼리를 기반으로 하는 R 데이터 소스 개체를 정의 합니다.
~~~~
RxSqlServerData(table=”airline”, connectionString = sqlConnString)
~~~~

~~~~
RxSqlServerData(sqlquery=”select [ArrDelay],[CRSDepTime],[DayOfWeek] from airlineWithIndex where rowNum <= 100000”, connectionString = sqlConnString)
~~~~ 

분석 알고리즘에 대량의 테이블의에서 데이터를 끌어오기 것이 중요에 제공 된 쿼리 되도록 `RxSqlServerData` 병렬 실행을 위해 최적화 됩니다. 병렬 실행 계획을 발생 하지 않는 쿼리는 계산에 대 한 단일 프로세스에서 발생할 수 있습니다.

[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 실행 계획을 분석 하 고 쿼리 성능을 향상 시킬 데 사용할 수 있습니다. 예를 들어 테이블에서 누락 된 인덱스는 쿼리를 실행 하는 데 걸리는 시간을 발생할 수 있습니다. 참조 [모니터링 및 성능 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md) 에 대 한 자세한 내용은 합니다.

쿼리에서 필요한 것 보다 더 많은 열을 검색할 때 성능에 영향을 줄 수 있는 다른 감독 합니다. 예를 들어 경우 수식을 3 개의 열을 기반으로 하며 테이블에 열이 30을 사용 하지 마십시오 쿼리 같은 `select *` 또는 필요한 것 보다 많은 열을 선택 하는 하나입니다.

> [!NOTE]
> 테이블을 쿼리 하는 대신 데이터 원본에 지정 된 경우 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 필요한 열이 테이블에서 인출할 수를 내부적으로 결정 됩니다; 그러나이 방법은 병렬 실행 시킬 수 있습니다.

## 알고리즘 매개 변수

많은 rx 학습 알고리즘은 학습 모델을 생성 하는 방식을 제어 하는 매개 변수를 지원 합니다. 모델의 정확성과 정확도 중요 한, 알고리즘의 성능을 만큼 중요 한 역할 수 있습니다. 계산의 속도를 높이려면 매개 변수인 모델 학습 매개 변수를 수정할 수 및 대부분의 경우에서 수 있습니다 나 정확성 저하 없이 성능을 향상 시킬 수 있습니다. 

예를 들어 `rxDTree` 지원는 `maxDepth` 최대 트리 깊이 제어 하는 매개 변수입니다. 으로 `maxDepth` 는 증가 하 고, 성능 저하 될 수 있습니다, 이므로 성능 영향 및 깊이 늘리는 경우의 혜택을 분석 하는 것이 중요 합니다. 

함께 사용할 수 있는 매개 변수 중 하나가 `rxLinMod` 및 `rxLogit` 는 `cube` 인수입니다. 수식의 첫 번째 종속 변수는 요소 변수의 경우이 인수를 사용할 수 있습니다. 경우 `cube` 로 설정 된 `TRUE`, 회귀 이루어집니다 분할된 역을 사용 하 여 더 빠르게 하 고 수 표준 회귀 계산 보다 메모리를 적게 사용 합니다. 수식에 많은 수의 변수, 성능 향상을 중요할 수 있습니다.

 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 사용자 가이드에 몇 가지 유용한 정보 다양 한 알고리즘에 적합 한 모델을 제어 합니다. 예를 들어, `rxDTree` 와 같은 매개 변수를 조정 하 여 시간 복잡성 및 예측 정확도 사이의 균형을 조정할 수 `maxNumBins`, `maxDepth`, `maxComplete`, 및 `maxSurrogate`합니다. 10 또는 15 이상에 깊이 늘리면 계산 비용이 매우 많이 할 수 있습니다.

에 대 한 성능 조정에 대 한 자세한 내용은 `rxDForest` 및 `rxDTree`, 참조 [성능 튜닝 옵션에 대 한 rxDForest/rxDTree](https://support.microsoft.com/kb/3104235)합니다.

## 모델 및 예측

일단 교육을 완료 하 고 선택 하는 가장 적합 한 모델, 좋습니다 예측에 사용할 수 있도록 모델 데이터베이스에 저장 합니다. 예측을 필요로 하는 온라인 트랜잭션 처리를 위해 미리 계산 된 모델의 예측에 대 한 데이터베이스에서 로드 매우 효율적입니다. 직렬화 하 고 모델 데이터베이스 테이블에 저장이 방법을 사용 하는 샘플 스크립트. 예측 모델은 데이터베이스에서 deserialize 합니다.

큰 데이터 집합을 사용 하는 경우에 특히 lm 또는 glm 등 알고리즘에 의해 생성 된 일부 모델은 크기가 매우 커질 수 있습니다. 에 저장 될 수 있는 데이터에 대 한 크기 제한이 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 데이터베이스에 저장 하기 전에 모델을 정리 해야 합니다.

> [!NOTE] 권장 하는 경우 저장 된 모델을 사용 하 여이 고 응용 프로그램에 분석을 통합 하는 빠른 예측은 중요 한 시나리오를 __DeployR__합니다. 웹, 데스크톱, 모바일 및 대시보드 응용 프로그램 내 R 분석을 쉽게 통합 사용할 수 있습니다. 특히,은 모델을 저장 하 고 다음 저장 된 모델을 사용 하 여 단일 행 예측을 수행 하는 데 적합 합니다. 자세한 내용은 참조 [에 대 한 DeployR](https://msdn.microsoft.com/microsoft-r/rserver/deployr-about)합니다.

## 관련 항목:
[리소스 관리](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
[리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)

[외부 리소스 풀 만들기](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server R 서비스 성능 조정 가이드](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [R 서비스에 대 한 SQL Server 구성](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [성능 사례 연구](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 