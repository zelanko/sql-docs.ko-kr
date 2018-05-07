---
title: sys.dm_pdw_sql_requests (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8fb8dc47d288470bedb8692ab38d00b0d810a1f6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  쿼리에서 SQL 단계의 일환으로 모든 SQL Server 쿼리 분포에 대 한 정보를 보유합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 SQL 쿼리 분배 속해 있는 쿼리의 고유 식별자입니다.<br /><br /> request_id, step_index, 및 distribution_id이이 보기에 대 한 키를 형성합니다.|참조에서 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 배포의 일부인 쿼리 단계의 인덱스입니다.<br /><br /> request_id, step_index, 및 distribution_id이이 보기에 대 한 키를 형성합니다.|step_index 참조 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|pdw_node_id|**int**|이 쿼리 분배 실행 되는 노드의 고유 식별자입니다.|참조에 대 한 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|distribution_id|**int**|이 쿼리 분배 실행 되는 배포의 고유 식별자입니다.<br /><br /> request_id, step_index, 및 distribution_id이이 보기에 대 한 키를 형성합니다.|distribution_id 참조 [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)합니다. 노드 범위 하지 배포 범위에서 실행 되는 요청에 대 한-1로 설정 합니다.|  
|상태|**nvarchar(32)**|쿼리 분포의 현재 상태입니다.|보류 중, 실행, 실패, 취소 됨, 완료, 중단, CancelSubmitted|  
|error_id|**nvarchar(36)**|오류의 고유 식별자 연관 된 쿼리 분배가 있는 경우.|참조에서 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)합니다. 오류가 발생 하지 않은 경우 NULL로 설정 합니다.|  
|start_time|**datetime**|배포에는 쿼리 실행을 시작한 시간입니다.|이 쿼리 분배 속한 작은 또는 현재 시간 및 크거나 start_time 쿼리 단계|  
|end_time|**datetime**|이 쿼리 분배 실행을 완료, 취소 되었거나 실패 시간입니다.|보다 크거나 시작 시간, 또는 진행 중이거나 대기 중인 쿼리 분포는 경우 NULL로 설정 합니다.|  
|total_elapsed_time|**int**|밀리초 단위로 쿼리 분배 실행 시간을 나타냅니다.|보다 크거나 0입니다. Start_time 델타 같음 및 end_time 완료, 실패 했거나 쿼리 배포를 취소 합니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건에는 "최 댓 값 초과 했습니다." 경고가 생성 됩니다.<br /><br /> 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
|row_count|**bigint**|행 개수 변경 하거나이 쿼리 분배 하 여 읽을 합니다.|변경 하거나 CREATE TABLE 및 DROP TABLE 등의 데이터를 반환 하지 않는 작업에 대 한-1입니다.|  
|spid|**int**|쿼리 분배를 실행 중인 SQL Server 인스턴스에서 세션 id입니다.||  
|command|**nvarchar(4000)**|전체 텍스트 쿼리 분배가에 대 한 명령입니다.|모든 유효한 요청 또는 쿼리 문자열입니다.|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에 최대 시스템 뷰의 값 섹션을 참조는 [최소값 및 최 댓 값 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) 항목입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
