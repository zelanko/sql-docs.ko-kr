---
description: sys.dm_db_xtp_index_stats(Transact-SQL)
title: sys.dm_db_xtp_index_stats (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 520452d4886d009777de62af55047ef3cd47caaf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474964"
---
# <a name="sysdm_db_xtp_index_stats-transact-sql"></a>sys.dm_db_xtp_index_stats(Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  데이터베이스를 마지막으로 다시 시작한 후 수집된 통계가 포함됩니다.  
  
 자세한 내용은 [메모리 내 OLTP &#40;In-Memory 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md) 및 [Memory-Optimized 테이블에서 인덱스를 사용 하기 위한 지침](/previous-versions/sql/sql-server-2016/dn133166(v=sql.130))을 참조 하세요.  

  
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
  
