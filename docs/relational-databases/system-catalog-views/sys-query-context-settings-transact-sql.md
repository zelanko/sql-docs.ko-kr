---
title: sys.query_context_settings (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS
- QUERY_CONTEXT_SETTINGS
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_context_settings catalog view
ms.assetid: 3c1887df-6bd8-491e-82fc-d25ad9589faf
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 3f1dbbc0ad525e8158949e538690552ea7463327
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39554053"
---
# <a name="sysquerycontextsettings-transact-sql"></a>sys.query_context_settings (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  쿼리와 관련 된 컨텍스트 설정에 영향을 주는 의미 체계에 대 한 정보를 포함 합니다. 사용할 수 있는 다양 한 상황에 맞는 설정 가지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (쿼리의 올바른 결과 정의) 쿼리 의미 체계에 영향을 하는 합니다. 다양 한 설정에서 컴파일된 동일한 쿼리 텍스트 (기본 데이터)에 따라 다른 결과 생성할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|기본 키입니다. 이 값은 쿼리에 대 한 실행 계획 XML에 노출 됩니다.|  
|**set_options**|**varbinary(8)**|여러 SET 옵션의 상태를 반영 하는 비트 마스크입니다. 자세한 내용은 [sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)합니다.|  
|**language_id**|**smallint**|언어의 id입니다. 자세한 내용은 [sys.syslanguages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)합니다.|  
|**date_format**|**smallint**|날짜 형식입니다. 자세한 내용은 [SET DATEFORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md)을 참조하세요.|  
|**date_first**|**tinyint**|첫 번째 날짜 값입니다. 자세한 내용은 [SET DATEFIRST&#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md)를 참조하세요.|  
|**상태**|**varbinary(2)**|쿼리 또는 쿼리가 실행 된 컨텍스트의 유형을 나타내는 비트 마스크 필드입니다. <br />열 값 (16 진수에서 표현) 여러 플래그의 조합 수 있습니다.<br /><br /> 0x0-일반 쿼리 (특정 플래그 없음)<br /><br /> 0x1-커서 Api 저장 프로시저 중 하나를 통해 실행 되는 쿼리<br /><br /> 0x2-알림에 대 한 쿼리<br /><br /> 0x4-내부 쿼리<br /><br /> 0x8-범용 매개 변수화 하지 않고 자동 매개 변수화 된 쿼리<br /><br /> 0x10-커서 인출 쿼리 새로 고침<br /><br /> 0x20-커서 업데이트 요청에 사용 되는 쿼리<br /><br /> 0x40-는 커서가 열릴 때 초기 결과 집합이 반환 됩니다 (자동 인출 커서)<br /><br /> 0x80 – 암호화 된 쿼리<br /><br /> 0x100 – 행 수준 보안 조건자의 컨텍스트에서 쿼리|  
|**required_cursor_options**|**int**|커서 유형과 같이 사용자가 지정한 커서 옵션입니다.|  
|**acceptable_cursor_options**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 문의 실행을 지원하도록 암시적으로 변환될 수 있는 커서 옵션입니다.|  
|**merge_action_type**|**smallint**|트리거 실행 계획의 결과로 사용할 유형의 **병합** 문입니다.<br /><br /> 0은 비 트리거 계획을 결과로 실행 되지 않는 트리거 계획을 **병합** 문이나의 결과로 실행 되는 트리거 계획을를 **병합** 만 를지정하는문을**삭제할** 작업 합니다.<br /><br /> 1는 **삽입** 결과로 실행 되는 트리거 계획을 **병합** 문입니다.<br /><br /> 2는 **업데이트** 결과로 실행 되는 트리거 계획을 **병합** 문입니다.<br /><br /> 3을 **삭제** 의 결과로 실행 되는 트리거 계획을 **병합** 해당 하는 포함 하는 문이 **삽입** 또는 **업데이트** 동작입니다.<br /><br /> <br /><br /> 연계 동작으로 실행 하는 중첩 트리거의 경우이 값은 작업을 **병합** 연계를 유발 하는 문입니다.|  
|**default_schema_id**|**int**|정규화 되지 않은 이름을 확인 하는 데 사용 되는 기본 스키마의 ID입니다.|  
|**is_replication_specific**|**bit**|복제에 사용 합니다.|  
|**is_contained**|**varbinary(1)**|1 포함된 된 데이터베이스를 나타냅니다.|  
  
## <a name="permissions"></a>사용 권한  
 필요 합니다 **VIEW DATABASE STATE** 권한.  
  
## <a name="see-also"></a>관련 항목  
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
