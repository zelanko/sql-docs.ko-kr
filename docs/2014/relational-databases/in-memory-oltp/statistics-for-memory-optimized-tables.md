---
title: 메모리 액세스에 최적화된 테이블에 대한 통계 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e47a8c6f5b0da31aea9168bbbc56bd9b28afb96
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63155798"
---
# <a name="statistics-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 대한 통계
  쿼리 최적화 프로그램에서는 열에 대한 통계를 사용하여 쿼리 성능을 향상시키는 쿼리 계획을 만듭니다. 통계는 데이터베이스의 테이블에서 수집되어 데이터베이스 메타데이터에 저장됩니다.  
  
 통계는 자동으로 생성되지만 수동으로 만들 수도 있습니다. 예를 들어, 인덱스 생성 시 해당 인덱스 키 열에 대한 통계가 자동으로 생성됩니다. 통계 생성에 대한 자세한 내용은 [Statistics](../statistics/statistics.md)를 참조하십시오.  
  
 일반적으로 통계 데이터는 행이 삽입, 업데이트 및 삭제되면서 시간이 지남에 따라 변경됩니다. 따라서 통계를 정기적으로 업데이트해야 합니다. 기본적으로 최적화 프로그램에서 통계가 최신 상태가 아닐 수 있다고 확인하면 디스크 기반 테이블에 대한 통계가 자동으로 업데이트됩니다.  
  
 메모리 최적화 테이블에 대한 통계는 기본적으로 업데이트되지 않습니다. 그 대신 이 통계를 수동으로 업데이트해야 합니다. 개별 열, 인덱스 또는 테이블에 대해 [UPDATE STATISTICS &#40;transact-sql&#41;](/sql/t-sql/statements/update-statistics-transact-sql) 를 사용 합니다. [Sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) 을 사용 하 여 데이터베이스의 모든 사용자 및 내부 테이블에 대 한 통계를 업데이트 합니다.  
  
 [CREATE statistics &#40;transact-sql&#41;](/sql/t-sql/statements/create-statistics-transact-sql) 또는 [UPDATE statistics &#40;transact-sql&#41;](/sql/t-sql/statements/update-statistics-transact-sql)를 사용 하는 경우 메모리 최적화 테이블에 대해 `NORECOMPUTE` 자동 통계 업데이트를 사용 하지 않도록 지정 해야 합니다. 디스크 기반 테이블의 경우 transact-sql [&#40;&#41;마지막 sp_updatestats ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)이후 테이블이 수정 된 경우에만 [sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) 에서 통계를 업데이트 합니다. 메모리 최적화 테이블의 경우 [sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) 는 항상 업데이트 된 통계를 생성 합니다. [sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) 는 메모리 최적화 테이블에 대 한 좋은 옵션입니다. 그렇지 않으면 통계를 개별적으로 업데이트할 수 있도록 중요 한 변경 내용이 있는 테이블을 알아야 합니다.  
  
 데이터를 샘플링하거나 전체 검사를 수행하여 통계를 생성할 수 있습니다. 샘플링된 통계만 테이블 데이터 샘플을 사용하여 데이터 분포를 예상합니다. 전체 검사 통계는 전체 테이블을 검사하여 데이터 분포를 결정합니다. 전체 검사 통계는 일반적으로 더 정확하지만 컴퓨팅하는 데 시간이 더 오래 걸립니다. 샘플링된 통계는 더 빠르게 수집할 수 있습니다.  
  
 디스크 기반 테이블은 샘플링된 통계를 기본적으로 사용합니다. 메모리 액세스에 최적화된 테이블만 전체 검사 통계를 지원합니다. [CREATE statistics &#40;transact-sql&#41;](/sql/t-sql/statements/create-statistics-transact-sql) 또는 [UPDATE statistics &#40;transact-sql&#41;](/sql/t-sql/statements/update-statistics-transact-sql)를 사용 하는 `FULLSCAN` 경우 메모리 최적화 테이블에 대 한 옵션을 지정 해야 합니다.  
  
 메모리 최적화 테이블 통계에 대한 추가 고려 사항:  
  
-   메모리 최적화 테이블의 인덱스는 테이블과 함께 만들어집니다. 인덱스 키 열에 대한 통계는 테이블이 비어 있을 때 생성됩니다. 따라서 데이터를 테이블에 로드한 후 이 통계를 업데이트해야 합니다.  
  
-   고유하게 컴파일된 저장 프로시저의 경우 프로시저를 컴파일할 때 프로시저의 쿼리에 대한 실행 계획이 최적화됩니다. 이 작업은 프로시저가 생성될 때와 서버가 다시 시작할 때만 수행되며 통계가 업데이트될 때는 수행되지 않습니다. 따라서 테이블에는 대표적인 데이터 집합이 포함되어야 하며 프로시저가 생성되기 전에 통계를 최신 상태로 업데이트해야 합니다. 데이터베이스를 오프라인 상태로 만들었다가 다시 온라인 상태로 만들거나, 서버를 다시 시작하면 고유하게 컴파일된 저장 프로시저가 다시 컴파일됩니다.  
  
## <a name="guidelines-for-statistics-when-deploying-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블을 배포할 때 통계에 대한 지침  
 쿼리 계획을 만들 때 쿼리 최적화 프로그램에 최신 통계가 사용되도록 다음 5단계를 사용하여 메모리 최적화 테이블을 배포합니다.  
  
1.  테이블과 인덱스를 만듭니다. 인덱스는 `CREATE TABLE` 문에서 인라인으로 지정됩니다.  
  
2.  테이블에 데이터를 로드합니다.  
  
3.  테이블에 대한 통계를 업데이트합니다.  
  
4.  테이블에 액세스하는 저장 프로시저를 만듭니다.  
  
5.  작업을 실행합니다. 작업에는 고유하게 컴파일된 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 저장 프로시저와 해석된 저장 프로시저의 혼합뿐 아니라 임시 일괄 처리도 포함될 수 있습니다.  
  
 데이터를 로드하고 통계를 업데이트한 후 고유하게 컴파일된 저장 프로시저를 만들면 메모리 최적화 테이블에 사용 가능한 통계가 최적화 프로그램에 사용됩니다. 프로시저를 컴파일할 때 효율적인 쿼리 계획을 수행할 수 있습니다.  
  
## <a name="guidelines-for-maintaining-statistics-on-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 통계를 유지 관리하기 위한 지침  
 통계를 최신 상태로 유지하려면 메모리 최적화 테이블에서 통계를 정기적으로 업데이트합니다.  
  
 데이터가 자주 변경되는 경우 통계를 자주 업데이트해야 합니다. 예를 들어, 일괄 업데이트 후 테이블 통계를 업데이트합니다. 업데이트된 통계의 장점을 이용할 수 있도록 통계를 업데이트한 후 고유하게 컴파일된 저장 프로시저를 삭제하고 다시 만듭니다.  
  
 .  
  
 최대 작업 중에는 통계를 업데이트하지 마십시오.  
  
 통계를 업데이트하려면:  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [통계 업데이트 태스크](../maintenance-plans/update-statistics-task-maintenance-plan.md) 를 사용 하 여 [유지 관리 계획을 만드는](../maintenance-plans/create-a-maintenance-plan.md) 데 사용  
  
-   또는 아래 설명과 같이 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 통해 통계를 업데이트합니다.  
  
 단일 메모리 최적화 테이블 (*myschema.xml*)에 대 한 통계를 업데이트 합니다. *Mytable*)에서 다음 스크립트를 실행 합니다.  
  
```  
UPDATE STATISTICS myschema.Mytable WITH FULLSCAN, NORECOMPUTE  
```  
  
 현재 데이터베이스에 있는 모든 메모리 최적화 테이블에 대한 통계를 업데이트하려면 다음 스크립트를 실행합니다.  
  
```sql  
DECLARE @sql NVARCHAR(MAX) = N''  
  
SELECT @sql += N'  
   UPDATE STATISTICS ' + quotename(schema_name(schema_id)) + N'.' + quotename(name) + N' WITH FULLSCAN, NORECOMPUTE'  
FROM sys.tables WHERE is_memory_optimized=1  
  
EXEC sp_executesql @sql  
```  
  
 데이터베이스의 모든 테이블에 대 한 통계를 업데이트 하려면 [transact-sql&#41;&#40;sp_updatestats ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)를 실행 합니다.  
  
 다음 예에서는 메모리 최적화 테이블의 통계가 마지막으로 업데이트된 시기를 보고합니다. 이 정보로 통계를 업데이트해야 할지 여부를 결정할 수 있습니다.  
  
```sql  
select t.object_id, t.name, sp.last_updated as 'stats_last_updated'  
from sys.tables t join sys.stats s on t.object_id=s.object_id cross apply sys.dm_db_stats_properties(t.object_id, s.stats_id) sp  
where t.is_memory_optimized=1  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화 된 테이블](memory-optimized-tables.md)  
  
  
