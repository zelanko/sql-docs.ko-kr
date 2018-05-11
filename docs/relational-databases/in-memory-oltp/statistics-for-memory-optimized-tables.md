---
title: 메모리 액세스에 최적화된 테이블에 대한 통계 | Microsoft 문서
ms.custom: ''
ms.date: 10/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7de6ceba5b5acc68b37abfcbbb991669981d200b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="statistics-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 대한 통계
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  쿼리 최적화 프로그램에서는 열에 대한 통계를 사용하여 쿼리 성능을 향상시키는 쿼리 계획을 만듭니다. 통계는 데이터베이스의 테이블에서 수집되어 데이터베이스 메타데이터에 저장됩니다.  
  
 통계는 자동으로 생성되지만 수동으로 만들 수도 있습니다. 예를 들어, 인덱스 생성 시 해당 인덱스 키 열에 대한 통계가 자동으로 생성됩니다. 통계 생성에 대한 자세한 내용은 [Statistics](../../relational-databases/statistics/statistics.md)를 참조하십시오.  
  
 일반적으로 통계 데이터는 행이 삽입, 업데이트 및 삭제되면서 시간이 지남에 따라 변경됩니다. 따라서 통계를 정기적으로 업데이트해야 합니다. 기본적으로 쿼리 최적화 프로그램에서 통계가 최신 상태가 아닐 수 있다고 확인하면 테이블에 대한 통계가 자동으로 업데이트됩니다.  
  
 메모리 최적화 테이블 통계에 대한 고려 사항:  
  
-   SQL Server 2016 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]부터 130 이상의 데이터베이스 호환성 수준을 사용하는 경우 메모리 최적화 테이블에 대한 통계 자동 업데이트가 지원됩니다. [ALTER DATABASE 호환성 수준(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요. 이전에 낮은 호환성 수준으로 만든 테이블이 데이터베이스에 있는 경우에는 통계를 수동으로 한 번 업데이트해야 이후에 통계가 자동으로 업데이트됩니다.
  
-   고유하게 컴파일된 저장 프로시저의 경우 프로시저를 컴파일할 때(만든 시간에 발생) 프로시저의 쿼리에 대한 실행 계획이 최적화됩니다. 통계가 업데이트될 때 자동으로 다시 컴파일되지 않습니다. 따라서 테이블에는 프로시저가 생성되기 전에 대표적인 데이터 집합이 포함되어야 합니다.  
  
-   고유하게 컴파일된 저장 프로시저는 [sp_recompile(TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)을 사용하여 수동으로 다시 컴파일할 수 있으며, 데이터베이스가 오프라인으로 전환되었다가 다시 온라인으로 전환된 경우 또는 데이터베이스가 장애 조치(failover)되거나 서버가 다시 시작된 경우 자동으로 다시 컴파일됩니다.  
  
## <a name="enabling-automatic-update-of-statistics-in-existing-tables"></a>기존 테이블의 통계 자동 업데이트 사용

호환성 수준이 130 이상인 데이터베이스에서 테이블을 만든 경우 해당 테이블의 모든 통계에 대해 자동 업데이트가 적용되며 추가 작업이 필요하지 않습니다.

이전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이전 버전 또는 130보다 낮은 호환성 수준에서 만든 메모리 최적화 테이블이 있는 경우에는 통계를 수동으로 한 번 업데이트해야 이후에 자동 업데이트가 적용됩니다.

이전 호환성 수준에서 생성된 메모리 최적화 테이블에 대해 통계 자동 업데이트를 사용하려면 다음 단계를 따르세요.

1. 데이터베이스 호환성 수준을 업데이트합니다. `ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL=130`

2. 메모리 최적화 테이블의 통계를 수동으로 업데이트합니다. 다음은 동일한 작업을 수행하는 샘플 스크립트입니다.

3. 업데이트된 통계를 활용하기 위해 고유하게 컴파일된 저장 프로시저를 수동으로 다시 컴파일합니다.


            *통계에 대한 일회성 스크립트:* 낮은 호환성 수준에서 만든 메모리 최적화 테이블에 대해 다음 TRANSACT-SQL 스크립트를 한 번 실행하여 메모리 최적화 모든 테이블의 통계를 업데이트하고 향후 통계 자동 업데이트를 사용하도록 설정합니다(AUTO_UPDATE_STATISTICS가 데이터베이스에 사용하도록 설정된 것으로 가정).

```
-- Assuming AUTO_UPDATE_STATISTICS is already ON for your database:
-- ALTER DATABASE CURRENT SET AUTO_UPDATE_STATISTICS ON;

ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL = 130;
GO
DECLARE @sql NVARCHAR(MAX) = N'';
SELECT
      @sql += N'UPDATE STATISTICS '
         + quotename(schema_name(t.schema_id))
         + N'.'
         + quotename(t.name)
         + ';' + CHAR(13) + CHAR(10)
   FROM sys.tables AS t
   WHERE t.is_memory_optimized = 1 AND 
        t.object_id IN (SELECT object_id FROM sys.stats WHERE no_recompute=1)
;
EXECUTE sp_executesql @sql;
GO
-- Each row appended to @sql looks roughly like:
-- UPDATE STATISTICS [dbo].[MyMemoryOptimizedTable];
```


            *자동 업데이트가 사용하도록 설정되어 있는지 확인:* 다음 스크립트는 메모리 최적화 테이블에 대한 통계에 자동 업데이트가 사용되는지 여부를 확인합니다. 이전 스크립트를 실행한 후 모든 통계 개체에 대한 `1` 열에 `auto-update enabled` 가 반환됩니다.

```
SELECT 
    quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) AS [table],
    s.name AS [statistics object],
    1-s.no_recompute AS [auto-update enabled]
FROM sys.stats s JOIN sys.tables o ON s.object_id=o.object_id
WHERE o.is_memory_optimized=1
```

## <a name="guidelines-for-deploying-tables-and-procedures"></a>테이블 및 프로시저 배포 지침  
 쿼리 계획을 만들 때 쿼리 최적화 프로그램에 최신 통계가 사용되도록 다음 4단계를 사용하여 메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저를 배포합니다.  
  
1.  데이터베이스의 호환성 수준이 130 이상인지 확인합니다. [ALTER DATABASE 호환성 수준(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.

2.  테이블과 인덱스를 만듭니다. 인덱스는 **CREATE TABLE** 문에서 인라인으로 지정되어야 합니다.  
  
3.  테이블에 데이터를 로드합니다.  
  
4.  테이블에 액세스하는 저장 프로시저를 만듭니다.  
  
 데이터를 로드한 후 고유하게 컴파일된 저장 프로시저를 만들면 메모리 최적화 테이블에 사용 가능한 통계가 최적화 프로그램에 사용됩니다. 프로시저를 컴파일할 때 효율적인 쿼리 계획을 수행할 수 있습니다.  

## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
