---
title: 메모리 내 OLTP에 대 한 시스템 뷰, 저장 프로시저, Dmv 및 대기 유형 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: efaa59e3-dbfa-407f-b1aa-cb0c6602ea17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d047cbc4fe3ba3f4945acd9da4f627a05992e779
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62842402"
---
# <a name="system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 시스템 보기, 저장 프로시저, DMV 및 대기 형식
  이 항목은 메모리 내 OLTP를 지원하는 많은 데이터베이스 개체에 대한 간략한 설명과 링크를 제공합니다.  
  
### <a name="system-views"></a>시스템 뷰  
  
|시스템 뷰|Description|메모리 내 OLTP 기능|  
|-----------------|-----------------|-----------------------------|  
|[data_spaces &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-data-spaces-transact-sql)|파일 그룹에 메모리 최적화 데이터가 있는지 확인 합니다.|다음 열에는 **형식** 및 **type_desc**추가 값이 표시 됩니다.|  
|[sys.indexes&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)|인덱스가 메모리 최적화 테이블에 있는지 확인합니다.|다음 열에는 **형식** 및 **type_desc**추가 값이 표시 됩니다.|  
|[sys. Transact-sql&#41;&#40;매개 변수](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)|고유하게 컴파일된 저장 프로시저를 보다 효율적으로 실행할 수 있도록 매개 변수가 null을 허용하지 않는지 확인합니다.|**is_nullable** 열입니다.|  
|[all_sql_modules &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql)|저장 프로시저가 고유하게 컴파일되었는지 확인합니다.|**uses_native_compilation** 열입니다.|  
|[sys.sql_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)|저장 프로시저가 고유하게 컴파일되었는지 확인합니다.|**uses_native_compilation** 열입니다.|  
|[table_types &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql)|테이블이 메모리 최적화되었는지 확인합니다.|**is_memory_optimized** 열입니다.|  
|[sys.tables&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|테이블이 메모리 최적화 되었는지 확인 하 고 테이블의 내구성 설정을 확인 합니다.|**내구성**, **durability_desc**및 **is_memory_optimized** 열.|  
|[hash_indexes &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-hash-indexes-transact-sql)|메모리 최적화 테이블의 해시 인덱스를 표시합니다.|메모리 내 OLTP에 특정합니다.|  
  
### <a name="metadata-functions"></a>메타데이터 함수  
  
|메타 데이터 함수|Description|메모리 내 OLTP 기능|  
|-----------------------|-----------------|-----------------------------|  
|[OBJECTPROPERTYEX&#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|데이터베이스 개체가 메모리 최적화되었는지 확인합니다.|**ExecIsWithNativeCompilation** 및 **Tableismemoryoptimized** 된 속성입니다.<br /><br /> **Isschemabound** 속성은 프로시저 개체 유형을 지원 합니다. NULL 대신 프로시저의 경우 0을 반환 합니다.|  
|[SERVERPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|서버에서 메모리 내 OLTP를 지원하는지 확인합니다.|**Isxtpsupported** 속성입니다.|  
  
### <a name="system-stored-procedures"></a>시스템 저장 프로시저  
  
|저장 프로시저|Description|  
|----------------------|-----------------|  
|[sys.sp_xtp_bind_db_resource_pool&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)|메모리 내 OLTP 데이터베이스를 리소스 풀로 바인딩합니다.|  
|[sp_xtp_checkpoint_force_garbage_collection &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-checkpoint-force-garbage-collection-transact-sql)|메모리 내 OLTP 데이터베이스에서 가비지 수집을 시작합니다.|  
|[sp_xtp_control_proc_exec_stats &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)|고유하게 컴파일된 저장 프로시저에 대한 통계 컬렉션을 설정합니다.|  
|[sp_xtp_control_query_exec_stats &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)|고유하게 컴파일된 저장 프로시저에 대한 쿼리당 통계 컬렉션을 설정합니다.|  
|[sp_xtp_merge_checkpoint_files &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)|데이터 및 델타 파일을 병합합니다.|  
|[sys.sp_xtp_unbind_db_resource_pool&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)|데이터베이스와 리소스 풀 간의 바인딩을 제거합니다.|  
  
## <a name="dynamic-management-views-dmvs"></a>동적 관리 뷰(DMV)  
 메모리 최적화 테이블에는 몇 가지 DMV가 있습니다.  
  
 자세한 내용은 메모리 액세스에 [최적화 된 테이블 동적 관리 뷰 &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql)를 참조 하세요.  
  
## <a name="wait-types"></a>대기 유형  
 메모리 내 OLTP를 지원하는 대기 유형이 몇 가지 있습니다.  
  
 자세한 내용은 **WAIT_XTP**시작 하는 대기 유형 및 [dm_os_wait_stats &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql) 항목에서 **xtpproc** 를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP는 메모리 내 최적화를 &#40;&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [메모리 내 OLTP에 대한 Transact-SQL 지원](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
