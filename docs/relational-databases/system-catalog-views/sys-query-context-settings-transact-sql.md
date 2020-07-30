---
title: sys. query_context_settings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2413e629e969fb0aa7dff93dc2959f1b7a007b10
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394021"
---
# <a name="sysquery_context_settings-transact-sql"></a>sys. query_context_settings (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  쿼리와 관련 된 컨텍스트 설정에 영향을 주는 의미 체계에 대 한 정보를 포함 합니다. 쿼리 의미 체계에 영향을 주는에서 사용할 수 있는 여러 컨텍스트 설정이 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (쿼리의 올바른 결과 정의). 다른 설정에서 컴파일된 동일한 쿼리 텍스트는 기본 데이터에 따라 다른 결과를 생성할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|기본 키입니다. 이 값은 쿼리를 위한 실행 계획 XML에 표시 됩니다.|  
|**set_options**|**varbinary(8)**|여러 SET 옵션의 상태를 반영 하는 비트 마스크입니다. 자세한 내용은 [dm_exec_plan_attributes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)을 참조 하십시오.|  
|**language_id**|**smallint**|언어의 id입니다. 자세한 내용은 [sys.sys언어 &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)를 참조 하세요.|  
|**date_format**|**smallint**|날짜 형식입니다. 자세한 내용은 [SET DATEFORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md)을 참조하세요.|  
|**date_first**|**tinyint**|날짜의 첫 번째 값입니다. 자세한 내용은 [SET DATEFIRST&#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md)를 참조하세요.|  
|**status**|**varbinary (2)**|쿼리가 실행 된 쿼리 또는 컨텍스트의 유형을 나타내는 비트 마스크 필드입니다. <br />열 값은 여러 플래그 (16 진수로 표현)의 조합일 수 있습니다.<br /><br /> 0x0-일반 쿼리 (특정 플래그 없음)<br /><br /> 0x1-커서 Api 저장 프로시저 중 하나를 통해 실행 된 쿼리<br /><br /> 0x2-알림에 대 한 쿼리<br /><br /> 0x4-내부 쿼리<br /><br /> 0x8-유니버설 매개 변수화를 사용 하지 않는 자동 매개 변수가 있는 쿼리<br /><br /> 0x10-커서 인출 새로 고침 쿼리<br /><br /> 0x20-커서 업데이트 요청에 사용 되는 쿼리<br /><br /> 0x40-커서를 열 때 초기 결과 집합이 반환 됩니다 (커서 자동 인출).<br /><br /> 0x80 암호화 쿼리<br /><br /> 0x100-행 수준 보안 조건자 컨텍스트의 쿼리|  
|**required_cursor_options**|**int**|커서 유형과 같이 사용자가 지정한 커서 옵션입니다.|  
|**acceptable_cursor_options**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 문의 실행을 지원하도록 암시적으로 변환될 수 있는 커서 옵션입니다.|  
|**merge_action_type**|**smallint**|**MERGE** 문의 결과로 사용 되는 트리거 실행 계획의 유형입니다.<br /><br /> 0은 트리거하지 않은 계획, **merge** 문의 결과로 실행 되지 않는 트리거 계획 또는 **DELETE** 동작만 지정 하는 **merge** 문의 결과로 실행 되는 트리거 계획을 나타냅니다.<br /><br /> 1은 **MERGE** 문의 결과로 실행 되는 **INSERT** 트리거 계획을 나타냅니다.<br /><br /> 2는 **MERGE** 문의 결과로 실행 되는 **UPDATE** 트리거 계획을 나타냅니다.<br /><br /> 3은 해당 **INSERT** 또는 **UPDATE** 동작을 포함 하는 **MERGE** 문의 결과로 실행 되는 **DELETE** 트리거 계획을 나타냅니다.<br /><br /> <br /><br /> 연계 동작에 의해 실행 되는 중첩 트리거의 경우이 값은 cascade를 발생 시킨 **MERGE** 문의 동작입니다.|  
|**default_schema_id**|**int**|정규화 되지 않은 이름을 확인 하는 데 사용 되는 기본 스키마의 ID입니다.|  
|**is_replication_specific**|**bit**|복제에 사용 됩니다.|  
|**is_contained**|**varbinary (1)**|1은 포함 된 데이터베이스를 나타냅니다.|  
  
## <a name="permissions"></a>사용 권한  
 **VIEW DATABASE STATE** 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [query_store_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
