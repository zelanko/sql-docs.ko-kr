---
title: 분류자 사용자 정의 함수 만들기 및 테스트 - Resource Governor
description: SQL Server Management Studio 쿼리 편집기에서 Transact-SQL 문 실행과 관련된 분류자 사용자 정의 함수를 만들고 테스트하는 방법을 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 07/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, classifier function create
- classifier function [SQL Server], test
- classifier function [SQL Server], create
- Resource Governor, classifier function test
ms.assetid: 7866b3c9-385b-40c6-aca5-32d3337032be
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d08ddba59acdf2692e8493a10bac58048458ae23
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506604"
---
# <a name="create-and-test-a-classifier-user-defined-function"></a>분류자 사용자 정의 함수 만들기 및 테스트
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  이 항목에서는 분류자 사용자 정의 함수(Transact-UDF)를 만들고 테스트하는 방법을 보여 줍니다. 이 단계에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 편집기에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 문을 실행하는 작업이 포함되어 있습니다.  
  
 아래 절차에 나오는 예에서는 매우 복잡한 분류자 사용자 정의 함수를 만드는 경우에 대해 설명합니다.  
  
 이 예제에서는 다음과 같습니다.  
  
-   지정한 시간 범위 동안의 프로덕션 처리를 위해 리소스 풀(pProductionProcessing) 및 작업 그룹(gProductionProcessing)을 만듭니다.  
  
-   프로덕션 처리에 대한 요구 사항에 맞지 않는 연결 처리를 위해 리소스 풀(pOffHoursProcessing) 및 작업 그룹(gOffHoursProcessing)을 만듭니다.  
  
-   로그인 시간에 대해 계산할 수 있는 시작 시간과 종료 시간을 보유하기 위해 마스터에 테이블(TblClassificationTimeTable)을 만듭니다. 리소스 관리자가 분류자 함수에 대한 스키마 바인딩을 사용하기 때문에 마스터에 이 테이블을 만들어야 합니다.  
  
    > [!NOTE]  
    >  가능하면 자주 업데이트하는 큰 테이블은 마스터에 저장하지 마십시오.  
  
 분류자 함수는 로그인 시간을 확장합니다. 과도하게 복잡한 함수를 사용하면 로그인을 수행할 때 시간이 초과되거나 빠른 연결 속도를 늦출 수 있습니다.  
  
## <a name="to-create-the-classifier-user-defined-function"></a>분류자 사용자 정의 함수를 만들려면  
  
1.  새 리소스 풀 및 작업 그룹을 만들고 구성합니다. 각 작업 그룹을 적합한 리소스 풀에 할당합니다.  
  
    ```sql  
    --- Create a resource pool for production processing  
    --- and set limits.  
    USE master;  
    GO  
    CREATE RESOURCE POOL pProductionProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 100,  
         MIN_CPU_PERCENT = 50  
    );  
    GO  
    
    --- Create a workload group for production processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gProductionProcessing  
    WITH  
    (  
         IMPORTANCE = MEDIUM  
    );  
    
    --- Assign the workload group to the production processing  
    --- resource pool.  
    USING pProductionProcessing  
    GO  
    
    --- Create a resource pool for off-hours processing  
    --- and set limits.  
    CREATE RESOURCE POOL pOffHoursProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 50,  
         MIN_CPU_PERCENT = 0  
    );  
    GO  
    
    --- Create a workload group for off-hours processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gOffHoursProcessing  
    WITH  
    (  
         IMPORTANCE = LOW  
    )  
    --- Assign the workload group to the off-hours processing  
    --- resource pool.  
    USING pOffHoursProcessing;  
    GO  
    ```  
  
2.  메모리 내 구성을 업데이트합니다.  
  
    ```sql  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    GO  
    ```  
  
3.  테이블을 만들고 프로덕션 처리 시간 범위의 시작 시간과 종료 시간을 정의합니다.  
  
    ```sql  
    USE master;  
    GO  
    CREATE TABLE tblClassificationTimeTable  
    (  
         strGroupName     sysname          not null,  
         tStartTime       time              not null,  
         tEndTime         time              not null  
    );  
    GO  
    --- Add time values that the classifier will use to  
    --- determine the workload group for a session.  
    INSERT into tblClassificationTimeTable VALUES('gProductionProcessing', '6:35 AM', '6:15 PM');  
    GO  
    ```  
  
4.  조회 테이블의 시간에 대해 계산될 수 있는 시간 함수 및 값을 사용하는 분류자 함수를 만듭니다. 분류자 함수에서 조회 테이블을 사용하는 방법에 대한 자세한 내용은 이 항목의 "분류자 함수에서 조회 테이블을 사용하는 최선의 구현 방법"을 참조하세요.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 에는 날짜 및 시간 데이터 형식 및 함수의 확장된 집합이 도입되었습니다. 자세한 내용은 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)를 참조하세요.  
  
    ```sql  
    CREATE FUNCTION fnTimeClassifier()  
    RETURNS sysname  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
    /* We recommend running the classifier function code under 
    snapshot isolation level OR using NOLOCK hint to avoid blocking on 
    lookup table. In this example, we are using NOLOCK hint. */
         DECLARE @strGroup sysname  
         DECLARE @loginTime time  
         SET @loginTime = CONVERT(time,GETDATE())  
         SELECT TOP 1 @strGroup = strGroupName  
              FROM dbo.tblClassificationTimeTable WITH(NOLOCK)
              WHERE tStartTime <= @loginTime and tEndTime >= @loginTime  
         IF(@strGroup is not null)  
         BEGIN  
              RETURN @strGroup  
         END  
    --- Use the default workload group if there is no match  
    --- on the lookup.  
         RETURN N'gOffHoursProcessing'  
    END;  
    GO  
    ```  
  
5.  분류자 함수를 등록하고 메모리 내 구성을 업데이트합니다.  
  
    ```sql  
    ALTER RESOURCE GOVERNOR with (CLASSIFIER_FUNCTION = dbo.fnTimeClassifier);  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    GO  
    ```  
  
## <a name="to-verify-the-resource-pools-workload-groups-and-the-classifier-user-defined-function"></a>리소스 풀, 작업 그룹 및 분류자 사용자 정의 함수를 확인하려면  
  
1.  다음 쿼리를 사용하여 리소스 풀 및 작업 그룹 구성을 가져옵니다.  
  
    ```sql  
    USE master;  
    SELECT * FROM sys.resource_governor_resource_pools;  
    SELECT * FROM sys.resource_governor_workload_groups;  
    GO  
    ```  
  
2.  다음 쿼리를 사용하여 분류자 함수가 존재하며 설정되었는지 확인합니다.  
  
    ```sql  
    --- Get the classifier function Id and state (enabled).  
    SELECT * FROM sys.resource_governor_configuration;  
    GO  
    --- Get the classifer function name and the name of the schema  
    --- that it is bound to.  
    SELECT   
          object_schema_name(classifier_function_id) AS [schema_name],  
          object_name(classifier_function_id) AS [function_name]  
    FROM sys.dm_resource_governor_configuration;  
    ```  
  
3.  다음 쿼리를 사용하여 리소스 풀 및 작업 그룹에 대한 현재 런타임 데이터를 가져옵니다.  
  
    ```sql  
    SELECT * FROM sys.dm_resource_governor_resource_pools;  
    SELECT * FROM sys.dm_resource_governor_workload_groups;  
    GO  
    ```  
  
4.  다음 쿼리를 사용하여 각 그룹에 있는 세션을 확인합니다.  
  
    ```sql  
    SELECT s.group_id, CAST(g.name as nvarchar(20)), s.session_id, s.login_time, 
        CAST(s.host_name as nvarchar(20)), CAST(s.program_name AS nvarchar(20))  
    FROM sys.dm_exec_sessions AS s  
    INNER JOIN sys.dm_resource_governor_workload_groups AS g  
        ON g.group_id = s.group_id  
    ORDER BY g.name;  
    GO  
    ```  
  
5.  다음 쿼리를 사용하여 각 그룹에 있는 요청을 확인합니다.  
  
    ```sql  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, 
        r.start_time, r.command, r.sql_handle, t.text   
    FROM sys.dm_exec_requests AS r  
    INNER JOIN sys.dm_resource_governor_workload_groups AS g  
        ON g.group_id = r.group_id  
    CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name;  
    GO  
    ```  
  
6.  다음 쿼리를 사용하여 분류자에서 실행하는 요청을 확인합니다.  
  
    ```sql  
    SELECT s.group_id, g.name, s.session_id, s.login_time, s.host_name, s.program_name   
    FROM sys.dm_exec_sessions AS s  
    INNER JOIN sys.dm_resource_governor_workload_groups AS g  
        ON g.group_id = s.group_id  
           AND 'preconnect' = s.status  
    ORDER BY g.name;  
    GO  
  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, 
        r.command, r.sql_handle, t.text   
    FROM sys.dm_exec_requests AS r  
    INNER JOIN sys.dm_resource_governor_workload_groups AS g  
        ON g.group_id = r.group_id  
           AND 'preconnect' = r.status  
     CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name;  
    GO  
    ```  
  
## <a name="best-practices-for-using-lookup-tables-in-a-classifier-function"></a>분류자 함수에서 조회 테이블을 사용하는 최선의 구현 방법  
  
1.  조회 테이블은 반드시 필요한 경우에만 사용합니다. 조회 테이블을 사용해야 하는 경우에는 함수 자체에 테이블을 하드 코딩할 수 있습니다. 그러나 이 경우에는 분류자 함수의 동적 변경 및 복잡도 간에 균형을 조정해야 합니다.  
  
2.  조회 테이블에 대해 수행되는 I/O를 제한합니다.  
  
    1.  `TOP 1`을 사용하여 행을 하나만 반환합니다.  
  
    2.  테이블의 행 수를 최소화합니다.  
  
    3.  테이블의 모든 행이 한 페이지 또는 소수의 페이지에 있도록 합니다.  
  
    4.  Index Seek 작업을 사용하여 찾은 행이 최대한 많은 찾기 열을 사용하는지 확인합니다.  
  
    5.  조인을 통해 여러 테이블을 사용하려는 경우에는 단일 테이블로 비정규화합니다.  
  
3.  조회 테이블에 대한 차단을 방지합니다.  
  
    1.  `NOLOCK` 힌트를 사용하여 차단을 방지하거나 함수에서 `SET LOCK_TIMEOUT`(최댓값 1,000밀리초)을 사용합니다.  
  
    2.  테이블은 반드시 master 데이터베이스에 있어야 합니다. 클라이언트 컴퓨터가 연결을 시도할 때 복구가 보장되는 데이터베이스는 master 데이터베이스뿐입니다.  
  
    3.  항상 스키마를 사용하여 테이블 이름을 정규화합니다. master 데이터베이스를 사용해야 하기 때문에 데이터베이스 이름은 필요하지 않습니다.  
  
    4.  테이블에 트리거를 사용하지 않습니다.  
  
    5.  테이블 콘텐츠를 업데이트하는 경우에는 기록기가 판독기를 차단하지 않도록 분류자 함수에서 스냅샷 격리 수준 트랜잭션을 사용합니다. `NOLOCK` 힌트를 사용해도 차단을 완화할 수 있습니다.  
  
    6.  가능한 경우 테이블 콘텐츠 변경 시 분류자 함수를 사용하지 않도록 설정합니다.  
  
        > [!WARNING]  
        >  이러한 최선의 구현 방법을 따르는 것이 좋습니다. 문제가 발생하여 최선의 구현 방법을 따를 수 없는 경우에는 Microsoft 지원 센터에 문의하여 향후 발생할 수 있는 문제를 예방하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [리소스 관리자 작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [템플릿을 사용하여 리소스 관리자 구성](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [리소스 관리자 속성 보기](../../relational-databases/resource-governor/view-resource-governor-properties.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
