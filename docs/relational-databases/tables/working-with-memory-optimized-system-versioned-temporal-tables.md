---
title: 메모리 액세스에 최적화된 시스템 버전 임시 테이블로 작업 | Microsoft 문서
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 691d4f80-6754-43f5-8b43-d4facf08f6fc
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 79b4be6319bda8c4b4a3563db8fc6ec027f2db9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783261"
---
# <a name="working-with-memory-optimized-system-versioned-temporal-tables"></a>메모리 액세스에 최적화된 시스템 버전 임시 테이블로 작업
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 메모리 최적화 시스템 버전 temporal 테이블로 작업하는 방식과 디스크 기반 시스템 버전 temporal 테이블로 작업하는 방식의 차이점에 대해 설명합니다.  
  
> [!NOTE]  
>  메모리 액세스에 최적화된 테이블을 임시로 사용하는 방식은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에만 적용되며 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에는 적용되지 않습니다.  
  
## <a name="discovering-metadata"></a>메타데이터 검색  
 메모리 최적화 시스템 버전의 temporal 테이블과 관련한 메타데이터를 검색하려면 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) 및 [sys.internal_tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md)의 정보를 결합해야 합니다. 시스템 버전 temporal 테이블은 내부 메모리 내 기록 테이블에 parent_object_id로 표시됩니다.  
  
 아래 예에는 이러한 테이블을 쿼리하고 조인하는 방법이 나와 있습니다.  
  
```  
SELECT SCHEMA_NAME (T1.schema_id) as TemporalTableSchema  
   , OBJECT_NAME(IT.parent_object_id) as TemporalTableName  
   , T1.object_id as TemporalTableObjectId  
   , IT.Name as InternalHistoryStagingName   
   , SCHEMA_NAME (T2.schema_id) as HistoryTableSchema  
   , OBJECT_NAME (T1.history_table_id) as HistoryTableName   
FROM sys.internal_tables IT    
JOIN sys.tables T1   
   ON IT.parent_object_id = T1.object_id   
JOIN sys.tables T2   
   ON T1.history_table_id = T2.object_id   
WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2  
  
```  
  
## <a name="modifying-data"></a>데이터 수정  
 시스템 버전 메모리 최적화 temporal 테이블은 고유하게 컴파일된 저장 프로시저를 통해 수정할 수 있으므로 메모리 최적화 비temporal 테이블을 시스템 버전 관리 테이블로 변환하고 기존의 고유한 저장 프로시저를 유지할 수 있습니다.  
  
 아래 예에는 앞에서 만든 테이블을 고유하게 컴파일된 모듈에서 수정할 수 있는 방법이 나와 있습니다.  
  
```  
CREATE PROCEDURE dbo.UpdateFXCurrencyPair  
   (   
       @ProviderID int  
     , @CurrencyID1 int  
     , @CurrencyID2 int  
     , @BidRate decimal(8,4)  
     , @AskRate decimal(8,4)   
   )   
WITH NATIVE_COMPILATION, SCHEMABINDING  
   , EXECUTE AS OWNER   
AS    
   BEGIN ATOMIC WITH   
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT  , LANGUAGE = N'English')   
      UPDATE dbo.FXCurrencyPairs SET AskRate = @AskRate, BidRate  = @BidRate   
     WHERE ProviderID = @ProviderID AND CurrencyID1 = @CurrencyID1 AND CurrencyID2 = @CurrencyID2   
END   
GO ;  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [메모리 액세스에 최적화된 시스템 버전 임시 테이블 만들기](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [메모리 액세스에 최적화된 시스템 버전 임시 테이블 모니터링](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 시스템 버전 임시 테이블 관련 성능 고려 사항](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
