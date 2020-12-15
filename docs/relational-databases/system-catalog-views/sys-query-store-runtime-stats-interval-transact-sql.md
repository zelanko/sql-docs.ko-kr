---
description: sys.query_store_runtime_stats_interval (Transact-sql)
title: sys.query_store_runtime_stats_interval (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_RUNTIME_STATS_INTERVAL
- SYS.QUERY_STORE_RUNTIME_STATS_INTERVAL
- QUERY_STORE_RUNTIME_STATS_INTERVAL_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS_INTERVAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_runtime_stats_interval catalog view
- query_store_runtime_stats_interval catalog view
ms.assetid: 2be83785-0569-41a3-88c8-59bfa0932e6e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 49c45098a319a3a9577fe5911ac1f5f0accc6990
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404453"
---
# <a name="sysquery_store_runtime_stats_interval-transact-sql"></a>sys.query_store_runtime_stats_interval (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  쿼리에 대 한 런타임 실행 통계 정보를 수집 하는 각 간격의 시작 및 종료 시간에 대 한 정보를 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_interval_id**|**bigint**|기본 키입니다.|
|**start_time**|**datetimeoffset**|기간의 시작 시간입니다.|
|**end_time**|**datetimeoffset**|기간의 종료 시간입니다.|
|**comment**|**nvarchar(32)**|항상 NULL입니다.|
  
## <a name="permissions"></a>사용 권한  
 **VIEW DATABASE STATE** 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sys.database_query_store_options &#40;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Transact-sql&#41;sys.query_context_settings &#40;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [Transact-sql&#41;sys.query_store_plan &#40;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [Transact-sql&#41;sys.query_store_query &#40;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [Transact-sql&#41;sys.query_store_query_text &#40;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [Transact-sql&#41;sys.query_store_runtime_stats &#40;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
