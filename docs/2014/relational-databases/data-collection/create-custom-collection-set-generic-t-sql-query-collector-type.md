---
title: 일반 T-SQL 쿼리 수집기 유형 (Transact SQL)를 사용 하는 사용자 지정 컬렉션 집합 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- T-SQL Query collector type
- collection sets [SQL Server], creating custom
ms.assetid: 6b06db5b-cfdc-4ce0-addd-ec643460605b
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8b93f05dce24f0da9b63cb7fc80a1328316eae7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274839"
---
# <a name="create-a-custom-collection-set-that-uses-the-generic-t-sql-query-collector-type-transact-sql"></a>일반 T-SQL 쿼리 수집기 유형을 사용하는 사용자 지정 컬렉션 집합 만들기(Transact-SQL)
  데이터 수집기와 함께 제공된 저장 프로시저를 사용하여 일반 T-SQL 쿼리 수집기 유형을 사용하는 컬렉션 항목을 포함하는 사용자 지정 컬렉션 집합을 만들 수 있습니다. 이 태스크를 수행하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 쿼리 편집기를 사용하여 다음 절차를 수행해야 합니다.  
  
-   업로드 일정 구성  
  
-   컬렉션 집합 정의 및 만들기  
  
-   컬렉션 항목 정의 및 만들기  
  
-   컬렉션 집합 및 컬렉션 항목의 존재 여부 확인  
  
> [!NOTE]  
>  사용자 지정 컬렉션 집합을 만들기 전에 데이터 컬렉션 매개 변수를 구성해야 합니다. 자세한 내용은 [데이터 컬렉션 매개 변수 구성&#40;Transact-SQL&#41;](configure-data-collection-parameters-transact-sql.md)을 참조하세요.  
  
### <a name="define-and-create-the-collection-set"></a>컬렉션 집합 정의 및 만들기  
  
1.  sp_syscollector_create_collection_set 저장 프로시저를 사용하여 새 컬렉션 집합을 정의합니다.  
  
    ```  
    USE msdb;  
    DECLARE @collection_set_id int;  
    DECLARE @collection_set_uid uniqueidentifier;  
    EXEC sp_syscollector_create_collection_set   
        @name=N'DMV Test 1',   
        @collection_mode=0,   
        @description=N'This is a test collection set',   
        @logging_level=1,   
        @days_until_expiration=14,   
        @schedule_name=N'CollectorSchedule_Every_15min',   
        @collection_set_id=@collection_set_id OUTPUT,   
        @collection_set_uid=@collection_set_uid OUTPUT;  
    SELECT @collection_set_id, @collection_set_uid;  
    ```  
  
     컬렉션 모드는 0(캐시됨) 또는 1(캐시 안 됨)로 설정할 수 있습니다.  
  
     로깅 수준은 0, 1 또는 2로 설정할 수 있습니다.  
  
     데이터 수집기와 함께 제공되는 미리 구성된 일정은 다음과 같습니다.  
  
    -   CollectorSchedule_Every_5min  
  
    -   CollectorSchedule_Every_10min  
  
    -   CollectorSchedule_Every_15min  
  
    -   CollectorSchedule_Every_30min  
  
    -   CollectorSchedule_Every_60min  
  
    -   CollectorSchedule_Every_6h  
  
     제공되는 일정 중 하나를 사용하지 않으려는 경우 새 일정을 만들어 컬렉션 집합에 대해 사용할 수 있습니다. 자세한 내용은 [일정을 만들고 작업에 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)을 참조하세요.  
  
### <a name="define-and-create-a-collection-item"></a>컬렉션 항목 정의 및 만들기  
  
1.  새 컬렉션 항목은 이미 설치된 일반 수집기 유형을 기반으로 하므로 다음 코드를 실행하여 일반 T-SQL 쿼리 수집기 유형에 해당하는 GUID를 설정할 수 있습니다.  
  
    ```tsql  
    DECLARE @collector_type_uid uniqueidentifier;  
    SELECT @collector_type_uid = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
    WHERE name = N'Generic T-SQL Query Collector Type';  
    DECLARE @collection_item_id int;  
    ```  
  
2.  sp_syscollector_create_collection_item 저장 프로시저를 사용하여 컬렉션 항목을 만듭니다. 일반 T-SQL 쿼리 수집기 유형에 필요한 스키마에 매핑되도록 컬렉션 항목에 대한 스키마를 선언합니다.  
  
    ```tsql  
    EXEC sp_syscollector_create_collection_item   
        @name=N'Query Stats - Test 1',   
        @parameters=N'  
            <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
            <Value>SELECT * FROM sys.dm_exec_query_stats</Value>  
            <OutputTable>dm_exec_query_stats</OutputTable>  
            </Query>  
            </ns:TSQLQueryCollector>',   
        @collection_item_id=@collection_item_id OUTPUT,   
        @frequency=5,   
        @collection_set_id=@collection_set_id,   
        @collector_type_uid=@collector_type_uid;  
    SELECT @collection_item_id;  
    ```  
  
### <a name="verify-that-the-new-collection-set-and-collection-item-exist"></a>새 컬렉션 집합 및 컬렉션 항목의 존재 여부 확인  
  
1.  새 컬렉션 집합을 시작하기 전에 다음 쿼리를 실행하여 새 컬렉션 집합 및 해당 컬렉션 항목이 생성되었는지 여부를 확인합니다.  
  
    ```tsql  
    USE msdb;  
    SELECT * FROM syscollector_collection_sets;  
    SELECT * FROM syscollector_collection_items;  
    GO  
    ```  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 직접 확인할 수도 있습니다. 개체 탐색기에서 **관리** 노드를 확장한 다음 **데이터 컬렉션**을 확장합니다. 새 컬렉션 집합이 표시됩니다. 컬렉션 집합의 아이콘에 있는 빨간색 원은 컬렉션 집합이 중지되었음을 나타냅니다.  
  
## <a name="example"></a>예제  
 다음 코드 예는 앞의 단계에 나와 있는 예제를 조합합니다. 컬렉션 집합 컬렉션 모드가 캐시됨 모드인 0으로 설정되어 있으므로 컬렉션 항목에 대해 설정된 컬렉션 빈도(5초)가 무시됩니다. 자세한 내용은 [Data Collection](data-collection.md)을 참조하세요.  
  
```tsql  
USE msdb;  
  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier  
  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'DMV Stats Test 1',  
    @collection_mode = 0,  
    @description = N'This is a test collection set',  
    @logging_level=1,  
    @days_until_expiration = 14,  
    @schedule_name=N'CollectorSchedule_Every_15min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
SELECT @collection_set_id,@collection_set_uid;  
  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = collector_type_uid FROM syscollector_collector_types   
WHERE name = N'Generic T-SQL Query Collector Type';  
  
DECLARE @collection_item_id int;  
EXEC sp_syscollector_create_collection_item  
@name= N'Query Stats - Test 1',  
@parameters=N'  
<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
<Query>  
  <Value>select * from sys.dm_exec_query_stats</Value>  
  <OutputTable>dm_exec_query_stats</OutputTable>  
</Query>  
 </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 5, -- This parameter is ignored in cached mode  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid;  
SELECT @collection_item_id;  
  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)   
 [일정 관리](../../ssms/agent/manage-schedules.md)   
 [컬렉션 집합 시작 또는 중지](start-or-stop-a-collection-set.md)  
  
  
