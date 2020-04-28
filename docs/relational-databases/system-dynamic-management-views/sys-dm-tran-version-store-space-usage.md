---
title: sys. dm_tran_version_store_space_usage (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a4fac732f784a401206f37fb2af9d3d8e0688ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68262659"
---
# <a name="sysdm_tran_version_store_space_usage-transact-sql"></a>sys. dm_tran_version_store_space_usage (Transact-sql)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

각 데이터베이스의 버전 저장소 레코드에서 사용 하는 tempdb의 총 공간을 표시 하는 테이블을 반환 합니다. **dm_tran_version_store_space_usage** 는 개별 버전 저장소 레코드를 탐색 하지 않으며 데이터베이스당 tempdb에 사용 된 집계 버전 저장소 공간을 반환 하므로 효율적이 고 실행 하는 데 비용이 많이 듭니다.
  
각 버전의 레코드는 이진 데이터로 저장 되 고 일부 추적 또는 상태 정보와 함께 저장 됩니다. 데이터베이스 테이블의 레코드와 마찬가지로 버전 저장소 레코드도 8192바이트 페이지로 저장됩니다. 레코드가 8192바이트를 초과하면 두 개의 레코드로 분할됩니다.  
  
버전 레코드는 이진 데이터로 저장되므로 각 데이터베이스의 다양한 데이터 정렬로 인한 문제가 발생하지 않습니다. **Dm_tran_version_store_space_usage** 를 사용 하 여 SQL Server 인스턴스에서 데이터베이스의 버전 저장소 공간 사용량에 따라 tempdb 크기를 모니터링 하 고 계획 합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|데이터베이스의 데이터베이스 ID입니다.|  
|**reserved_page_count**|**bigint**|데이터베이스의 버전 저장소 레코드에 대해 tempdb에 예약 된 페이지의 총 수입니다.|  
|**reserved_space_kb**|**bigint**|데이터베이스의 버전 저장소 레코드에 대해 tempdb에서 사용 된 총 공간 (kb)입니다.|  
  
## <a name="permissions"></a>사용 권한  
에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   

## <a name="examples"></a>예  
다음 쿼리를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 각 데이터베이스의 버전 저장소에서 tempdb에 사용 되는 공간을 확인할 수 있습니다. 
  
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
 
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
