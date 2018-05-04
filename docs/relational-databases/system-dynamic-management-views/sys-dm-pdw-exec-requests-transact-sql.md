---
title: sys.dm_pdw_exec_requests (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f6ceea1c7a604b2bfd98a158b383814990644391
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  현재 또는 최근에서 활성 상태인 모든 요청에 대 한 정보를 보유 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다. 요청/쿼리 당 한 개의 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 보기에 대 한 키입니다. 이 요청과 관련 된 고유 숫자 id입니다.|시스템의 모든 요청에 대해 고유 합니다.|  
|session_id|**nvarchar(32)**|이 쿼리가 실행 된 세션에 연결 된 고유 숫자 id입니다. 참조 [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)합니다.||  
|상태|**nvarchar(32)**|요청의 현재 상태입니다.|' 실행 중 ', '일시 중단', '완료', '취소', '실패'입니다.|  
|submit_time|**datetime**|요청을 제출한 실행 시간입니다.|유효한 **datetime** 작거나 현재 시간과 start_time 합니다.|  
|start_time|**datetime**|요청 실행을 시작한 시간입니다.|큐에 대기 중인된 요청;에 대 한 NULL 그렇지 않으면, 유효한 **datetime** 현재 시간 보다 작거나 합니다.|  
|end_compile_time|**datetime**|엔진은 완료 된 시간입니다 컴파일 요청 합니다.|아직; 컴파일되지 않은 요청에 대 한 NULL 그렇지 않은 경우 유효한 **datetime** start_time 보다 작은 및 현재 시간입니다.|
|end_time|**datetime**|시간을 요청 실행 완료, 실패 또는 취소 되었습니다.|활성 또는 대기 중인 요청;에 대 한 null 그렇지 않은 경우 유효한 **datetime** 현재 시간 보다 작거나 합니다.|  
|total_elapsed_time|**int**|밀리초 단위로 요청이 시작 된 이후 실행에 경과한 시간입니다.|0 사이의 start_time 및 end_time 간의 차이입니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건에는 "최 댓 값 초과 했습니다." 경고가 생성 됩니다.<br /><br /> 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
|레이블|**nvarchar(255)**|일부 선택 쿼리 문과 연결 된 선택적 레이블 문자열입니다.|모든 문자열 포함 된 ' a-z', ' A-Z', ' 0-9', '_'.|  
|error_id|**nvarchar(36)**|있는 경우 요청을와 연결 된 오류의 고유 id입니다.|참조 [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); 오류가 발생 하지 않은 경우 NULL로 설정 합니다.|  
|database_id|**int**|명시적 컨텍스트 (예: 사용 DB_X)에서 사용 하는 데이터베이스의 식별자입니다.|참조 id에 [sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)합니다.|  
|command|**nvarchar(4000)**|사용자가 제출한 요청의 전체 텍스트를 포함 합니다.|모든 유효한 쿼리 또는 요청 텍스트입니다. 4000 바이트를 초과 하는 쿼리는 잘립니다.|  
|resource_class|**nvarchar(20)**|이 요청에 대 한 리소스 클래스입니다. 관련 참조 **concurrency_slots_used** 에 [sys.dm_pdw_resource_waits &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)합니다.|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은 "최소 및 최대 값"를 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
## <a name="permissions"></a>Permissions  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="security"></a>보안  
 sys.dm_pdw_exec_requests는 데이터베이스 관련 사용 권한에 따라 쿼리 결과 필터링 하지 않습니다. VIEW SERVER STATE 권한이 있는 로그인 결과 모든 데이터베이스에 대 한 쿼리 결과 가져올 수 있습니다.  
  
> [!WARNING]  
>  공격자는 sys.dm_pdw_exec_requests를 사용 하 여 단순히 VIEW SERVER STATE 권한이 필요 하 고 있는 데이터베이스 관련 권한이 없다는 하 여 특정 데이터베이스 개체에 대 한 정보를 검색할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
