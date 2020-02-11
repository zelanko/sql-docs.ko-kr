---
title: 메모리 액세스에 최적화된 테이블이 있는 데이터베이스를 리소스 풀에 연결 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f222b1d5-d2fa-4269-8294-4575a0e78636
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d64b5bf6b60f37bf386840031c304dd5b13faaeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63158805"
---
# <a name="bind-a-database-with-memory-optimized-tables-to-a-resource-pool"></a>메모리 액세스에 최적화된 테이블이 있는 데이터베이스를 리소스 풀에 바인딩
  리소스 풀은 관리할 수 있는 물리적 리소스의 하위 집합을 나타냅니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스는 기본 리소스 풀의 리소스에 바인딩되고 이 리소스를 사용합니다. 하나 이상의 메모리 최적화 테이블에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 리소스를 사용하지 않고 다른 메모리 사용자가 메모리 최적화 테이블에 필요한 메모리를 사용하지 않게 하려면 별도의 리소스 풀을 만들어 메모리 최적화 테이블이 있는 데이터베이스의 메모리 사용을 관리해야 합니다.  
  
 하나의 리소스 풀에서만 데이터베이스를 바인딩할 수 있습니다. 하지만 동일한 풀에 여러 데이터베이스를 바인딩할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 메모리 최적화 테이블을 리소스 풀에 바인딩할 수 있지만 이렇게 하는 것은 아무 효과도 없습니다. 나중에 데이터베이스에 메모리 최적화 테이블을 만들려면 명명된 리소스 풀에 데이터베이스를 바인딩합니다.  
  
 데이터베이스를 리소스 풀에 바인딩하려면 먼저 데이터베이스와 리소스 풀이 있어야 합니다. 다음에 데이터베이스를 온라인 상태로 전환할 때 바인딩이 적용됩니다. 자세한 내용은 [Database States](../databases/database-states.md) 을 참조하세요.  
  
 리소스 풀에 대한 자세한 내용은 [Resource Governor Resource Pool](../resource-governor/resource-governor-resource-pool.md)을 참조하십시오.  
  
  
## <a name="create-the-database-and-resource-pool"></a>데이터베이스 및 리소스 풀 만들기  
 어떤 순서로든 데이터베이스와 리소스 풀을 만들 수 있습니다. 중요한 점은 데이터베이스를 리소스 풀에 바인딩하기 전에 데이터베이스와 리소스 풀이 모두 있는 것입니다.  
  
### <a name="create-the-database"></a>데이터베이스 만들기  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 하나 이상의 메모리 최적화 테이블이 포함되는 IMOLTP_DB라는 데이터베이스를 만듭니다. 이 명령을 실행하기 전에 \<driveAndPath> 경로가 있어야 합니다.  
  
```sql  
CREATE DATABASE IMOLTP_DB  
GO  
ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_fg CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_fg' , FILENAME = 'c:\data\IMOLTP_DB_fg') TO FILEGROUP IMOLTP_DB_fg;  
GO  
```  
  
### <a name="determine-the-minimum-value-for-min_memory_percent-and-max_memory_percent"></a>MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT의 최소값 결정  
 메모리 최적화 테이블에 필요한 메모리를 결정한 후에는 필요한 사용 가능 메모리 비율을 결정하고 해당 값 이상으로 메모리 비율을 설정합니다.  
  
 **예제:**    
이 예에서는 메모리 최적화 테이블 및 인덱스에 16GB의 메모리가 필요하며, 32GB의 메모리를 사용할 수 있게 커밋했다고 가정합니다.  
  
 얼핏 보기에는 MIN_MEMORY_PERCENT와 MAX_MEMORY_PERCENT를 50(16은 32의 50%)으로 설정하면 될 것 같습니다.  그러나 이렇게 설정하면 메모리 최적화 테이블에서 사용할 수 있는 메모리가 부족합니다. 아래 표([메모리 최적화 테이블 및 인덱스에 사용 가능한 메모리 비율](#percent-of-memory-available-for-memory-optimized-tables-and-indexes))에서 커밋된 메모리가 32GB인 경우 이 중 80%는 메모리 최적화 테이블과 인덱스에 사용할 수 있습니다.  따라서 커밋된 메모리가 아니라 사용 가능한 메모리를 기준으로 최소 및 최대 비율을 계산합니다.  
  
 `memoryNeedeed = 16`   
 `memoryCommitted = 32`   
 `availablePercent = 0.8`   
 `memoryAvailable = memoryCommitted * availablePercent`   
 `percentNeeded = memoryNeeded / memoryAvailable`  
  
 실수 연결:   
`percentNeeded = 16 / (32 * 0.8) = 16 / 25.6 = 0.625`  
  
 따라서 메모리 최적화 테이블 및 인덱스의 16GB 요구 사항을 충족하려면 사용 가능한 메모리의 62.5% 이상이 필요합니다.  MIN_MEMORY_PERCENT 맟 MAX_MEMORY_PERCENT 값은 정수여야 하므로 63% 이상으로 설정합니다.  
  
### <a name="create-a-resource-pool-and-configure-memory"></a>리소스 풀 만들기 및 메모리 구성  
 메모리 최적화 테이블의 메모리를 구성할 때 용량 계획은 MAX_MEMORY_PERCENT가 아니라 MIN_MEMORY_PERCENT를 기준으로 해야 합니다.  MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT에 대한 자세한 내용은 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql)을 참조하세요. 이렇게 하면 MIN_MEMORY_PERCENT로 인해 다른 리소스 풀에 대한 메모리 압력이 발생하여 메모리가 확실히 적용되므로 메모리 최적화 테이블의 메모리 가용성을 보다 효율적으로 예측할 수 있습니다. 메모리를 사용할 수 있고 OOM(메모리 부족) 조건을 방지할 수 있도록 하려면 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 값이 동일해야 합니다. 커밋된 메모리의 양에 따라 메모리 최적화 테이블에 사용 가능한 메모리의 비율은 아래 [메모리 최적화 테이블 및 인덱스에 사용 가능한 메모리 비율](#percent-of-memory-available-for-memory-optimized-tables-and-indexes) 을 참조하세요.  
  
 VM 환경에서 작업할 때 자세한 내용은 [최선의 구현 방법: VM 환경에서 메모리 내 OLTP 사용](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) 을 참조하세요.  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드에서는 메모리의 절반을 사용할 수 있는 Pool_IMOLTP라는 리소스 풀을 만듭니다.  풀이 만들어진 후 Pool_IMOLTP를 포함하도록 리소스 관리자가 다시 구성됩니다.  
  
```sql  
-- set MIN_MEMORY_PERCENT and MAX_MEMORY_PERCENT to the same value  
CREATE RESOURCE POOL Pool_IMOLTP   
  WITH   
    ( MIN_MEMORY_PERCENT = 63,   
    MAX_MEMORY_PERCENT = 63 );  
GO  
  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="bind-the-database-to-the-pool"></a>풀에 데이터베이스 바인딩  
 시스템 함수 `sp_xtp_bind_db_resource_pool` 을 사용하여 리소스 풀에 데이터베이스를 바인딩합니다. 이 함수는 데이터베이스 이름과 리소스 풀 이름의 2개의 매개 변수를 사용합니다.  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서는 리소스 풀 Pool_IMOLTP와 데이터베이스 IMOLTP_DB의 바인딩을 정의합니다. 데이터베이스를 온라인 상태로 전환할 때까지 바인딩이 적용되지 않습니다.  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
 시스템 함수 sp_xtp_bind_db_resourece_pool은 database_name과 pool_name이라는 두 개의 문자열 매개 변수를 사용합니다.  
  
## <a name="confirm-the-binding"></a>바인딩 확인  
 IMOLTP_DB의 리소스 풀 ID에 주의하여 바인딩을 확인합니다. 값이 NULL이면 안 됩니다.  
  
```sql  
SELECT d.database_id, d.name, d.resource_pool_id  
FROM sys.databases d  
GO  
```  
  
## <a name="make-the-binding-effective"></a>바인딩 적용  
 바인딩을 리소스 풀에 바인딩한 후 바인딩을 적용하려면 데이터베이스를 오프라인 상태로 만들었다가 다시 온라인 상태로 만들어야 합니다. 데이터베이스가 다른 풀에 바인딩된 경우 이전 리소스 풀에서 할당된 메모리가 제거되고 이제 데이터베이스로 새로 바인딩된 리소스 풀에서 메모리 최적화 테이블과 인덱스에 대한 메모리 할당이 수행됩니다.  
  
```sql  
USE master  
GO  
  
ALTER DATABASE IMOLTP_DB SET OFFLINE  
GO  
ALTER DATABASE IMOLTP_DB SET ONLINE  
GO  
  
USE IMOLTP_DB  
GO  
```  
  
 이제 데이터베이스가 리소스 풀에 바인딩됩니다.  
  
## <a name="change-min-memory-percent-and-max-memory-percent-on-an-existing-pool"></a>기존 풀에서 최소 메모리% 및 최대 메모리 비율 변경  
 서버에 메모리를 더 추가하거나 메모리 최적화 테이블에 필요한 메모리 양이 변경되면 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 값을 수정해야 합니다. 다음 단계에서는 리소스 풀에서 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT의 값을 변경하는 방법을 보여 줍니다. MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT에 사용할 값에 대한 지침은 아래 섹션을 참조하십시오.  자세한 내용은 [최선의 구현 방법: VM 환경에서 메모리 내 OLTP 사용](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) 항목을 참조하세요.  
  
1.  `ALTER RESOURCE POOL` 을 사용해서 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 값을 모두 변경합니다.  
  
2.  `ALTER RESURCE GOVERNOR` 를 사용하여 새 값으로 리소스 관리자를 다시 구성합니다.  
  
 **예제 코드**  
  
```sql  
ALTER RESOURCE POOL Pool_IMOLTP  
WITH  
     ( MIN_MEMORY_PERCENT = 70,  
       MAX_MEMORY_PERCENT = 70 )   
GO  
  
-- reconfigure the Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
## <a name="percent-of-memory-available-for-memory-optimized-tables-and-indexes"></a>메모리 최적화 테이블 및 인덱스에 사용 가능한 메모리 비율  
 메모리 최적화 테이블과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 동일한 리소스 풀에 매핑하면 리소스 관리자는 풀 사용자가 풀 사용에서 충돌을 일으키지 않도록 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 사용에 대한 내부 임계값을 설정합니다. 일반적으로 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 사용에 대한 임계값은 풀의 약 80%입니다. 다음 표에서는 다양한 메모리 크기에 대한 실제 임계값을 보여 줍니다.  
  
 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 데이터베이스의 전용 리소스 풀을 만드는 경우 행 버전과 데이터 증가율을 고려한 후 메모리 내 테이블에 필요한 물리적 메모리 양을 추정해야 합니다. 필요한 메모리를 추정했으면 DMV `sys.dm_os_sys_info`에서 ‘committed_target_kb’ 열에 반영된 대로 SQL 인스턴스의 커밋 대상 메모리 비율을 사용하여 리소스 풀을 만듭니다([sys.dm_os_sys_info](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql) 참조). 예를 들어, 인스턴스에 사용할 수 있는 총 메모리의 40%로 리소스 풀 P1을 만들 수 있습니다. 이 40%에서 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 엔진은 더 적은 비율을 사용하여 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 데이터를 저장합니다.  이는 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 에서 이 풀의 메모리를 모두 사용하지 않도록 하기 위한 것입니다.  이 비율 값은 대상에 커밋된 메모리에 따라 다릅니다. 다음 테이블은 OOM 오류가 발생하기 전 리소스 풀(명명된 또는 기본값)의 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 데이터베이스에서 사용할 수 있는 메모리에 대해 설명합니다.  
  
|대상에 커밋된 메모리|메모리 내 테이블에서 사용할 수 있는 비율|  
|-----------------------------|---------------------------------------------|  
|<= 8GB|70%|  
|<= 16GB|75%|  
|<= 32GB|80%|  
|\<= 96GB|85%|  
|>96GB|90%|  
  
 예를 들어, ‘대상에 커밋된 메모리’가 100GB인 경우 메모리 최적화 테이블과 인덱스에 60GB의 메모리가 필요한 것으로 추정한 다음, MAX_MEMORY_PERCENT = 67(60GB의 필요량/0.90 = 66.667GB – 67GB로 반올림됨. 67GB/100GB의 설치량 = 67%)의 리소스 풀을 만들어 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 개체에 필요한 60GB를 확보하도록 할 수 있습니다.  
  
 데이터베이스가 명명된 리소스 풀에 바인딩되면 다음 쿼리를 사용하여 다른 리소스 풀 전반의 메모리 할당량을 확인합니다.  
  
```sql  
SELECT pool_id  
     , Name  
     , min_memory_percent  
     , max_memory_percent  
     , max_memory_kb/1024 AS max_memory_mb  
     , used_memory_kb/1024 AS used_memory_mb   
     , target_memory_kb/1024 AS target_memory_mb  
   FROM sys.dm_resource_governor_resource_pools  
```  
  
 이 샘플 출력은 리소스 풀(PoolIMOLTP)에서 메모리 최적화 개체가 가져온 메모리가 1356MB이고 상한이 2307MB임을 보여 줍니다. 이 상한은 사용자와 이 풀에 매핑된 시스템 메모리 최적화 개체에서 가져올 수 있는 총 메모리를 제어합니다.  
  
 **샘플 출력**   
다음은 위에서 만든 데이터베이스 및 테이블의 결과입니다.  
  
```  
pool_id     Name        min_memory_percent max_memory_percent max_memory_mb used_memory_mb target_memory_mb  
----------- ----------- ------------------ ------------------ ------------- -------------- ----------------   
1           internal    0                  100                3845          125            3845  
2           default     0                  100                3845          32             3845  
259         PoolIMOLTP 0                  100                3845          1356           2307  
```  
  
 자세한 내용은 [sys.dm_resource_governor_resource_pools(Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql)를 참조하세요.  
  
 데이터베이스를 명명된 리소스 풀에 바인딩하지 않으면 ‘기본’ 풀에 바인딩됩니다. 기본 리소스 풀은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 대다수의 다른 할당에 사용되므로 DMV sys.dm_resource_governor_resource_pools를 사용하여 원하는 데이터베이스에 대해 메모리 최적화 테이블에서 사용하는 메모리를 모니터링할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.sp_xtp_bind_db_resource_pool&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)   
 [sys.sp_xtp_unbind_db_resource_pool&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)   
 [리소스 관리자](../resource-governor/resource-governor.md)   
 [리소스 관리자 리소스 풀](../resource-governor/resource-governor-resource-pool.md)   
 [리소스 풀 만들기](../resource-governor/create-a-resource-pool.md)   
 [리소스 풀 설정 변경](../resource-governor/change-resource-pool-settings.md)   
 [리소스 풀 삭제](../resource-governor/delete-a-resource-pool.md)  
  
  
