---
title: "카디널리티 추정(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: b6d6655b1640eff66182c78ea919849194d9714c
ms.openlocfilehash: 2d334f4397fdbf4097adbbc75d284202fd0fd8df
ms.contentlocale: ko-kr
ms.lasthandoff: 10/05/2017

---
# <a name="cardinality-estimation-sql-server"></a>카디널리티 추정(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  
이 문서에서는 SQL 시스템에 대한 최상의 CE(카디널리티 추정) 구성을 평가 및 선택하는 방법을 보여 줍니다. 대부분의 시스템에서는 가장 정확한 최신 CE를 활용합니다. CE는 쿼리에서 반환될 행 수를 예측합니다. 카디널리티 예측은 쿼리 최적화 프로그램에서 최적의 쿼리 계획을 생성하는 데 사용됩니다. 보다 정확한 추정을 통해 쿼리 최적화 프로그램은 일반적으로 최적의 쿼리 계획을 생성하는 작업을 더 잘 수행할 수 있습니다.  
  
응용 프로그램 시스템에서 새 CE로 인해 중요 쿼리의 계획이 더 느린 계획으로 변경될 수 있습니다. 이러한 쿼리는 다음 중 하나일 수 있습니다.  
  
- 여러 인스턴스가 동시에 자주 실행되는 OLTP(온라인 트랜잭션 처리) 쿼리  
- OLTP 업무 시간 중 많은 집계가 실행되는 SELECT  
  
새 CE보다 느리게 실행되는 쿼리를 확인할 수 있습니다. 또한 성능 문제를 해결하는 방법에 대한 옵션도 있습니다.  
  
  
## <a name="versions-of-the-ce"></a>CE 버전  
  
 1998년 Microsoft SQL Server 7.0에서 호환성 수준 70으로 CE가 크게 업데이트되었습니다. 이후 업데이트는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 시작되었으며 호환성 수준 120 이상을 의미합니다. 수준 120 이상의 CE 업데이트는 최신 데이터 웨어하우징 및 OLTP 워크로드에서 잘 작동하는 가정 및 알고리즘을 통합합니다.  
  
 **호환성 수준:** [COMPATIBILITY_LEVEL](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)에 대해 다음 Transact-SQL 코드를 사용하여 데이터베이스가 특정 수준에 있는지 확인할 수 있습니다.  

```tsql  
SELECT ServerProperty('ProductVersion');  
go  
  
ALTER DATABASE <yourDatabase>  
    SET COMPATIBILITY_LEVEL = 130;  
go  
  
SELECT d.name, d.compatibility_level  
    FROM sys.databases AS d  
    WHERE d.name = 'yourDatabase';  
go  
```  
  
 호환성 수준 120 이상으로 설정된 SQL Server 데이터베이스의 경우 [추적 플래그 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)을 활성화하면 시스템에서 CE 버전 70이 사용됩니다.  
  
 **레거시 CE:** 호환성 수준 120 이상으로 설정된 SQL Server 데이터베이스의 경우 [데이터베이스 범위 구성 변경](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 사용하여 데이터베이스 수준에서 CE 버전 70을 활성화할 수 있습니다.
  
```tsql  
ALTER DATABASE
    SCOPED CONFIGURATION  
        SET LEGACY_CARDINALITY_ESTIMATION = ON;  
go  
  
SELECT name, value  
    FROM sys.database_scoped_configurations  
    WHERE name = 'LEGACY_CARDINALITY_ESTIMATION';  
```  
 
 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)`USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION')`를 사용할 수 있습니다.
 
 ```tsql  
SELECT CustomerId, OrderAddedDate  
    FROM OrderTable  
    WHERE OrderAddedDate >= '2016-05-01'; 
    OPTION (USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION'));  
```
 
 **쿼리 저장소:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 처음 도입된 쿼리 저장소는 쿼리의 성능을 검사하는 유용한 도구입니다. 쿼리 저장소가 사용하도록 설정된 경우 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]의 데이터베이스 노드 아래에 있는 **개체 탐색기**에 **쿼리 저장소** 노드가 표시됩니다.  
  
```tsql  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE = ON;  
go  
  
SELECT  
        q.actual_state_desc AS [actual_state_desc-ofQueryStore],  
        q.desired_state_desc,  
        q.query_capture_mode_desc  
    FROM  
        sys.database_query_store_options  AS q;  
go  
  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE CLEAR;  
```  
  
 > [!TIP] 
 > [Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)의 최신 릴리스를 설치하고 종종 업데이트하는 것이 좋습니다.  
  
 카디널리티 추정 프로세스를 추적하기 위한 또 다른 옵션은 확장 이벤트 **query_optimizer_estimate_cardinality**를 사용하는 것입니다. 다음 T-SQL 코드 샘플은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행됩니다. C:\Temp\(경로 변경 가능)에 .xel 파일을 씁니다. [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]에서 .xel 파일을 열면 사용자에게 친숙한 방식으로 세부 정보가 표시됩니다.  
  
```tsql  
DROP EVENT SESSION Test_the_CE_qoec_1 ON SERVER;  
go  
  
CREATE EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    ADD EVENT sqlserver.query_optimizer_estimate_cardinality  
    (  
        ACTION (sqlserver.sql_text)  
            WHERE (  
                sql_text LIKE '%yourTable%'  
                and sql_text LIKE '%SUM(%'  
            )  
    )  
    ADD TARGET package0.asynchronous_file_target   
        (SET  
            filename = 'c:\temp\xe_qoec_1.xel',  
            metadatafile = 'c:\temp\xe_qoec_1.xem'  
        );  
go  
  
ALTER EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    STATE = START;  --STOP;  
go  
```  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]용 확장 이벤트에 대한 자세한 내용은 [SQL Database의 확장 이벤트](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)를 참조하세요.  
  
  
## <a name="steps-to-assess-the-ce-version"></a>CE 버전 평가 단계  
  
 다음 단계를 사용하여 가장 중요한 쿼리의 성능이 최신 CE에서 저하되는지 평가할 수 있습니다. 일부 단계는 이전 섹션에 표시되는 코드 샘플을 실행하여 수행됩니다.  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]를 엽니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 가장 높은 호환성 수준으로 설정되어 있는지 확인합니다.  
  
2.  다음 예비 단계를 수행합니다.  
  
    1.  [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]를 엽니다.  
  
    2.  T-SQL을 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 가장 높은 호환성 수준으로 설정되어 있는지 확인합니다.  
  
    3.  데이터베이스에서 해당 `LEGACY_CARDINALITY_ESTIMATION` 구성이 OFF로 설정되었는지 확인합니다.  
  
    4.  쿼리 저장소를 지웁니다. 물론 쿼리 저장소가 ON 상태인지 확인합니다.  
  
    5.  `SET NOCOUNT OFF;` 문을 실행합니다.  
  
3.  `SET STATISTICS XML ON;` 문을 실행합니다.  
  
4.  중요한 쿼리를 실행합니다.  
  
5.  결과 창의 **메시지** 탭에서 영향 받는 실제 행 수를 확인합니다.  
  
6.  결과 창의 **결과** 탭에서 XML 형식의 통계가 포함된 셀을 두 번 클릭합니다. 그래픽 쿼리 계획이 표시됩니다.  
  
7.  그래픽 쿼리 계획의 첫 번째 상자를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
8.  나중에 다른 구성과 비교하기 위해 다음 속성 값을 기록합니다.  
  
    -   **CardinalityEstimationModelVersion**  
  
    -   **예상 행 수**  
  
    -   **예상 I/O 비용**및 행 수 예측이 아닌 실제 성능과 관련된 여러 유사 *예상* 속성  
  
    -   **논리 연산** 및 **물리적 연산**. *병렬 처리* 로 설정하는 것이 좋습니다.  
  
    -   **실제 실행 모드**. *행* 보다 *일괄 처리*로 설정하는 것이 좋습니다.  
  
9. 예상 행 수와 실제 행 수를 비교합니다. CE의 부정확도 단위가 1%(높거나 낮음)인가요, 아니면 10%인가요?  
  
10. `SET STATISTICS XML OFF;`를 실행합니다.  
  
11. T-SQL을 실행하여 데이터베이스의 호환성 수준을 한 수준(예: 130 -> 120) 낮춥니다.  
  
12. 모든 비 임시 단계를 다시 실행합니다.  
  
13. 두 실행에서 CE 속성 값을 비교합니다.  
  
    - 최신 CE의 부정확도가 이전 CE보다 낮은가요?  
  
14. 마지막으로 두 실행의 다양한 성능 속성 값을 비교합니다.  
  
    -   쿼리에서 서로 다른 두 개의 CE 추정에서 다른 계획을 사용했나요?  
  
    -   최신 CE에서 쿼리가 더 느리게 실행되었나요?  
  
    -   이전 CE의 다른 계획을 사용할 때 쿼리 실행률이 더 향상되지 않는 한 대부분의 경우 최신 CE를 사용하는 것이 좋습니다.  
  
    -   그러나 쿼리가 이전 CE의 계획을 사용할 때 더 빠르게 실행되는 경우 시스템에서 더 빠른 계획을 사용하도록 하고 CE를 무시하는 것이 좋습니다. 이러한 방식으로 모든 쿼리에 최신 CE를 사용하면서 필요한 경우 더 빠른 계획을 유지할 수 있습니다.  
  
## <a name="how-to-activate-the-best-query-plan"></a>최상의 쿼리 계획을 활성화하는 방법  
  
새로운 CE를 사용할 경우 쿼리에 대해 더 느린 쿼리 계획이 생성된다고 가정합니다. 이러한 경우 더 빠른 계획을 활성화해야 하는 몇 가지 옵션이 있습니다.  
  
전체 데이터베이스에 대해 호환성 수준을 최신보다 더 낮게 설정할 수 있습니다.  
  
- 이렇게 하면 레거시 CE가 활성화되지만 모든 쿼리가 정확도가 떨어지는 이전 CE에 종속됩니다.  
  
- 또한 이전 수준 호환성은 쿼리 최적화 프로그램의 향상된 기능을 사용할 수 없습니다.  
  
`LEGACY_CARDINALITY_ESTIMATION`을 사용하면 전체 데이터베이스에서 이전 CE 또는 특정 쿼리만 사용면서 쿼리 최적화 프로그램의 향상된 기능을 사용할 수 있습니다.  
  
최상의 제어를 위해 테스트 중 SQL 시스템에서 이전 CE를 사용하여 생성된 계획을 사용하도록 *설정*할 수 있습니다. 원하는 계획을 *고정* 한 다음 전체 데이터베이스에서 최신 호환성 수준 및 CE를 사용하도록 설정할 수 있습니다. 옵션은 다음에 자세하게 설명합니다.  
  
### <a name="how-to-force-a-particular-query-plan"></a>특정 쿼리 계획을 강제로 실행하는 방법  
  
쿼리 저장소는 시스템에서 특정 쿼리 계획을 사용하도록 설정할 수 있는 다양한 방법을 제공합니다.  
  
- **sp_query_store_force_plan**을 실행합니다.  
  
- [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]에서 **쿼리 저장소** 노드를 확장하고 **리소스를 가장 많이 사용하는 노드**를 마우스 오른쪽 단추로 클릭한 다음 **리소스를 가장 많이 사용하는 노드 보기**를 클릭합니다. **계획 강제 적용** 및 **계획 강제 적용 해제**라는 레이블이 있는 단추가 표시됩니다.  
  
 쿼리 저장소에 대한 자세한 내용은 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)을 참조하세요.  
  
  
## <a name="examples-of-ce-improvements"></a>CE 개선 사례  
  
이 섹션에서는 최신 릴리스의 CE에 구현된 향상 기능을 활용하는 쿼리 예제를 설명합니다. 사용자가 특정 작업을 수행할 필요가 없는 배경 정보입니다.  
  
### <a name="example-a-ce-understands-maximum-value-might-be-higher-than-when-statistics-were-last-gathered"></a>예제 A. CE는 통계가 마지막으로 수집되었을 때보다 최대값이 더 높을 수 있다는 것을 인식합니다.  
  
OrderTable에 대한 통계가 마지막으로 수집된 날짜가 2016-04-30이고 최대 OrderAddedDate가 2016-04-30이라고 가정합니다. 호환성 수준 120 이상의 CE는 *오름차순* 데이터를 가진 OrderTable의 열에 통계에 의해 기록된 최대값보다 더 큰 값이 있을 수 있다는 것을 이해합니다. 이러한 인식은 다음과 같은 SQL SELECT에 대한 쿼리 계획을 향상시킵니다.  
  
```tsql  
SELECT CustomerId, OrderAddedDate  
    FROM OrderTable  
    WHERE OrderAddedDate >= '2016-05-01';  
```  
  
### <a name="example-b-ce-understands-that-filtered-predicates-on-the-same-table-are-often-correlated"></a>예제 B. CE는 동일한 테이블에 대해 필터링된 예측이 종종 서로 연관된다는 것을 이해합니다.  
  
다음 SELECT에는 Model 및 ModelVariant에 대해 필터링된 조건자가 있습니다. Model이 'Xbox'일 때 Xbox에 One이라는 변형이 있다면 ModelVariant가 'One'일 가능성이 있음을 직관적으로 이해할 수 있습니다.  
  
수준 120의 CE는 동일한 테이블의 두 열 Model 및 ModelVariant 간에 상호 연결이 있을 수 있다는 것을 이해합니다. CE는 쿼리에 의해 반환될 행 수를 더 정확하게 예측하고 쿼리 최적화 프로그램에서 더 최적의 계획을 생성합니다.  
  
```tsql  
SELECT Model, Purchase_Price  
    FROM dbo.Hardware  
    WHERE  
        Model  = 'Xbox'  AND  
        ModelVariant = 'One';  
```  
  
### <a name="example-c-ce-no-longer-assumes-any-correlation-between-filtered-predicates-from-different-tablescc"></a>예제 C. CE에서 더 이상 서로 다른 테이블의 필터링된 예측이 상호 연결되어 있다고 가정하지 않습니다. 
최신 작업 및 실제 비즈니스 데이터에 대한 새로운 연구 결과 서로 다른 테이블의 예측 필터는 보통 서로 상호 연결되지 않습니다. 다음 쿼리에서는 CE가 s.type 및 r.date가 서로 연결되지 않은 것으로 간주합니다. 따라서 CE는 반환 행 수를 더 적게 예측합니다.  
  
```tsql  
SELECT s.ticket, s.customer, r.store  
    FROM  
                   dbo.Sales    AS s  
        CROSS JOIN dbo.Returns  AS r  
    WHERE  
        s.ticket = r.ticket  AND  
        s.type   = 'toy'     AND  
        r.date   = '2016-05-11';  
```  
  
  
## <a name="see-also"></a>참고 항목  
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  [SQL Server 2014 카디널리티 추정기로 쿼리 계획 최적화](http://msdn.microsoft.com/library/dn673537.aspx)  
 [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)  
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)

