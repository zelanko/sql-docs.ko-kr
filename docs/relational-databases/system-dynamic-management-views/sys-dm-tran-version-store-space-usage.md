---
title: sys.dm_tran_version_store_space_usage (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: "10"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: cfdd2caa03fdd12501580c2584d68f374ee54222
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

각 데이터베이스에 대 한 버전 저장소 레코드에서 사용 하는 tempdb의 총 사용 공간을 표시 하는 테이블을 반환 합니다. **sys.dm_tran_version_store_space_usage** 효율적인 및 고성능 개별 버전 저장소를 통해 이동 하지 않는 동일 하 게 실행 기록 데이터베이스당 tempdb에 사용 되는 집계 된 버전 저장소 공간을 반환 합니다.
  
각 버전 레코드는 일부 추적/상태 정보와 함께 이진 데이터로 저장됩니다. 데이터베이스 테이블의 레코드와 마찬가지로 버전 저장소 레코드도 8192바이트 페이지로 저장됩니다. 레코드가 8192바이트를 초과하면 두 개의 레코드로 분할됩니다.  
  
버전 레코드는 이진 데이터로 저장되므로 각 데이터베이스의 다양한 데이터 정렬로 인한 문제가 발생하지 않습니다. 사용 하 여 **sys.dm_tran_version_store_space_usage** SQL Server 인스턴스에 있는 데이터베이스의 버전 저장소 공간 사용량에 따라 tempdb 크기를 모니터링 하 고 계획 합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|데이터베이스의 데이터베이스 ID입니다.|  
|**reserved_page_count**|**bigint**|데이터베이스의 레코드를 저장 하는 버전에 대 한 tempdb에 예약 된 페이지의 총 수입니다.|  
|**reserved_space_kb**|**bigint**|데이터베이스의 레코드를 저장 하는 버전에 대 한 tempdb에 (킬로바이트)에 사용 된 총 공간입니다.|  
  
## <a name="permissions"></a>Permissions  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   

## <a name="examples"></a>예  
 다음 쿼리는 SQL Server 인스턴스의 각 데이터베이스의 버전 저장소를 여 tempdb에 사용 되는 공간을 결정 하 사용할 수 있습니다. 
  
```sql  
SELECT 
  DB_NAME(database_id) as 'Database Name',
  reserved_page_count,
  reserved_space_kb 
FROM sys.dm_tran_version_store_space_usage;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Database Name            reserved_page_count reserved_space_kb  
------------------------ -------------------- -----------  
msdb                      0                    0             
AdventureWorks2016        10                   80             
AdventureWorks2016DW      0                    0             
WideWorldImporters        20                   160             
```
 
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
