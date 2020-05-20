---
title: sys. dm_db_xtp_index_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_index_stats
- dm_db_xtp_index_stats
- sys.dm_db_xtp_index_stats_TSQL
- dm_db_xtp_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_index_stats dynamic management view
ms.assetid: 8d0a50b8-2015-4576-930f-e3307dfc888e
author: CarlRabeler
ms.author: carlrab
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aeb38baa9671366f7291828e662afed30ad999f8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830832"
---
# <a name="sysdm_db_xtp_index_stats-transact-sql"></a>sys.dm_db_xtp_index_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  데이터베이스를 마지막으로 다시 시작한 후 수집된 통계가 포함됩니다.  
  
 자세한 내용은 메모리 내 [OLTP &#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md) 및 [메모리 최적화 테이블에서 인덱스 사용에 대 한 지침](https://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b)을 참조 하세요.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|이 인덱스가 속한 개체의 ID입니다.|  
|xtp_object_id|**bigint**|개체의 현재 버전에 해당 하는 내부 ID입니다.<br /><br /> 참고:에 적용 됩니다 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] .|  
|index_id|**bigint**|인덱스의 ID입니다. index_id는 프로젝트 내에서만 고유합니다.|  
|scans_started|**bigint**|수행된 메모리 내 OLTP 인덱스 검사 수입니다. 모든 SELECT, INSERT, UPDATE 또는 DELETE에는 인덱스 검사가 필요합니다.|  
|scans_retries|**bigint**|다시 시도해야 하는 인덱스 검사 수입니다.|  
|rows_returned|**bigint**|테이블을 만든 후 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 후 반환된 누적 행 수입니다.|  
|rows_touched|**bigint**|테이블을 만든 후 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 후 액세스된 누적 행 수입니다.|  
|rows_expiring|**bigint**|내부 전용입니다.|  
|rows_expired|**bigint**|내부 전용입니다.|  
|rows_expired_removed|**bigint**|내부 전용입니다.|  
|phantom_scans_started|**bigint**|내부 전용입니다.|  
|phatom_scans_retries|**bigint**|내부 전용입니다.|  
|phantom_rows_touched|**bigint**|내부 전용입니다.|  
|phantom_expiring_rows_encountered|**bigint**|내부 전용입니다.|  
|phantom_expired_rows_encountered|**bigint**|내부 전용입니다.|  
|phantom_expired_removed_rows_encountered|**bigint**|내부 전용입니다.|  
|phantom_expired_rows_removed|**bigint**|내부 전용입니다.|  
|object_address|**varbinary(8)**|내부 전용입니다.|  
  
## <a name="permissions"></a>사용 권한  
 현재 데이터베이스에 대해 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 최적화 테이블 동적 관리 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
