---
title: "컬렉션 집합에 컬렉션 항목 추가(Transact-SQL) | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collection items [SQL Server]
- collection sets [SQL Server], adding items
ms.assetid: 9fe6454e-8c0e-4b50-937b-d9871b20fd13
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 08104faa0f62ace56b291bc6fa45290e826b773b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="add-a-collection-item-to-a-collection-set-transact-sql"></a>컬렉션 집합에 컬렉션 항목 추가(Transact-SQL)
  데이터 수집기와 함께 제공되는 저장 프로시저를 사용하여 기존 컬렉션 집합에 컬렉션 항목을 추가할 수 있습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 편집기를 사용하여 다음 단계를 수행해야 합니다.  
  
### <a name="add-a-collection-item-to-a-collection-set"></a>컬렉션 집합에 컬렉션 항목 추가  
  
1.  **sp_syscollector_stop_collection_set** 저장 프로시저를 실행하여 항목을 추가할 컬렉션 집합을 중지합니다. 예를 들어, "Test Collection Set"라는 컬렉션 집합을 중지하려면 다음 문을 실행합니다.  
  
    ```tsql  
    USE msdb  
    DECLARE @csid int  
    SELECT @csid = collection_set_id  
    FROM syscollector_collection_sets  
    WHERE name = 'Test Collection Set'  
    SELECT @csid  
    EXEC dbo.sp_syscollector_stop_collection_set @collection_set_id = @csid  
    ```  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 사용하여 컬렉션 집합을 중지할 수도 있습니다. 자세한 내용은 [컬렉션 집합 시작 또는 중지](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)를 참조하세요.  
  
2.  컬렉션 항목을 추가하려는 컬렉션 집합을 선택합니다. 다음 코드에서는 컬렉션 집합 ID를 선언하는 방법을 보여 줍니다.  
  
    ```tsql  
    DECLARE @collection_set_id_1 int  
    SELECT @collection_set_id_1 = collection_set_id FROM [msdb].[dbo].[syscollector_collection_sets]  
    WHERE name = N'Test Collection Set'; -- name of collection set  
    ```  
  
3.  수집기 유형을 선언합니다. 다음 코드에서는 일반 T-SQL 쿼리 수집기 유형을 선언하는 방법을 보여 줍니다.  
  
    ```tsql  
    DECLARE @collector_type_uid_1 uniqueidentifier  
    SELECT @collector_type_uid_1 = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
       WHERE name = N'Generic T-SQL Query Collector Type';  
    ```  
  
     다음 코드를 실행하여 설치된 수집기 유형의 목록을 가져옵니다.  
  
    ```tsql  
    USE msdb  
    SELECT * from syscollector_collector_types  
    GO  
    ```  
  
4.  **sp_syscollector_create_collection_item** 저장 프로시저를 실행하여 컬렉션 항목을 만듭니다. 원하는 수집기 유형에 필요한 스키마에 매핑되도록 컬렉션 항목에 대한 스키마를 선언해야 합니다. 다음 예제에서는 일반 T-SQL 쿼리 입력 스키마를 사용합니다.  
  
    ```tsql  
    DECLARE @collection_item_id int;  
    EXEC [msdb].[dbo].[sp_syscollector_create_collection_item]   
    @name=N'OS Wait Stats', --name of collection item  
    @parameters=N'  
    <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
     <Query>  
      <Value>select * from sys.dm_os_wait_stats</Value>  
      <OutputTable>os_wait_stats</OutputTable>  
    </Query>  
    </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 60,  
    @collection_set_id = @collection_set_id_1, --- Provides the collection set ID number  
    @collector_type_uid = @collector_type_uid_1 -- Provides the collector type UID  
    SELECT @collection_item_id     
    ```  
  
5.  업데이트된 컬렉션 집합을 시작하기 전에 다음 쿼리를 실행하여 새 컬렉션 항목이 만들어졌는지 확인합니다.  
  
    ```xaml  
    USE msdb  
    SELECT * from syscollector_collection_sets  
    SELECT * from syscollector_collection_items  
    GO  
    ```  
  
     컬렉션 집합 및 해당 컬렉션 항목은 **결과** 탭에 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [일반 T-SQL 쿼리 수집기 유형을 사용하는 사용자 지정 컬렉션 집합 만들기&#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
