---
title: sys.dm_exec_distributed_requests (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b2a8da4e2bb2da05e13b8c603653a5401aeb1c2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  현재 또는 최근 활성 PolyBase 쿼리에서 모든 요청에 대 한 정보를 보유합니다. 요청/쿼리 당 한 개의 행을 나열합니다.  
  
 세션에 따라 한 요청 ID, 사용자 수 다음 검색 sys.dm_exec_distributed_requests 통해 – 실행할 생성 실제 분산된 요청 합니다. 예를 들어 일반 SQL 및 외부 SQL 테이블을 포함 하는 쿼리에서 분할할 것 다양 한 계산 노드에서 실행 하는 다양 한 문을/요청 합니다. 모든 계산 노드에 걸쳐 분산된 하는 단계를 추적 하려면 각각 하나의 특정 요청 및 연산자와 관련 된 계산 노드에서 모든 작업을 추적 하는 데 사용할 수 있는 'global' 실행 ID를 소개 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|이 보기에 대 한 키입니다. 이 요청과 관련 된 고유 숫자 id입니다.|시스템의 모든 요청에 대해 고유 합니다.|  
|execution_id|**nvarchar(32**|이 쿼리가 실행 된 세션에 연결 된 고유 숫자 id입니다.||  
|상태|**nvarchar(32**|요청의 현재 상태입니다.|'보류 중', '승인', 'AcquireSystemResources', 'Initializing', '구문 분석', 'AquireResources', '실행 중', '취소', ' 계획' 'Complete', ' 실패 ', '취소'.|  
|error_id|**nvarchar(36)**|있는 경우 요청을와 연결 된 오류의 고유 id입니다.|오류가 발생 하지 않은 경우 NULL로 설정 합니다.|  
|start_time|**datetime**|요청 실행을 시작한 시간입니다.|큐에 대기 중인된 요청;에 대 한 0 현재 시간 보다 작거나의 경우는 올바른 datetime입니다.|  
|end_time|**datetime**|엔진은 완료 된 시간입니다 컴파일 요청 합니다.|활성 또는 대기 중인 요청;에 대 한 null 그렇지 않은 경우 현재 시간 보다 작거나 유효한 datetime입니다.|  
|total_elapsed_time|**int**|밀리초 단위로 요청이 시작 된 이후 실행에 경과한 시간입니다.|0 사이의 start_time 및 end_time 간의 차이입니다. Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건에는 "최 댓 값 초과 했습니다." 경고가 생성 됩니다. 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 동적 관리 뷰를 사용한 문제 해결](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
