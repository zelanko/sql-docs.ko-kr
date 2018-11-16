---
title: sys.dm_exec_distributed_requests (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c02ea165ceec8af546d092d955e9275dcc96b240
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661192"
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  현재 또는 최근에 활성 PolyBase 쿼리에서 모든 요청에 대 한 정보를 보유합니다. 요청/쿼리 당 하나의 행을 나열합니다.  
  
 요청 ID, 사용자를 검색할 수도 있습니다 실행할 – sys.dm_exec_distributed_requests를 통해 생성 된 실제 분산된 요청 및 세션 기반 합니다. 예를 들어 일반 SQL 및 외부 SQL 테이블을 포함 하는 쿼리에서 다양 한 계산 노드에서 실행 하는 다양 한 문을/요청으로 분해할 수 됩니다. 모든 계산 노드 간에 분산된 하는 단계를 추적 하려면 각각 하나의 특정 요청 및 연산자와 관련 된 계산 노드에서 모든 작업을 추적 하는 '전역' 실행 ID를 소개 하겠습니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|이 보기에 대 한 키입니다. 요청과 연결 된 고유 숫자 id입니다.|시스템의 모든 요청에서 고유 합니다.|  
|execution_id|**nvarchar(32**|이 쿼리를 실행 하는 세션에 연결 된 고유 숫자 id입니다.||  
|상태|**nvarchar(32**|요청의 현재 상태입니다.|'보류 중', '권한 부여'를 'AcquireSystemResources', 'Initializing', '계획', '구문 분석', 'AquireResources', '실행 중', '취소'를 'Complete', ' 실패 '취소'.|  
|error_id|**nvarchar(36)**|있는 경우, 요청과 연결 된 오류의 고유 id입니다.|오류가 발생 하지 않은 경우 NULL로 설정 합니다.|  
|start_time|**datetime**|요청 실행을 시작한 시간입니다.|큐에 대기 중인된 요청에 대 한 0 현재 작거나의 그렇지 않으면, 유효한 datetime입니다.|  
|end_time|**datetime**|엔진은 요청 컴파일 완료 하는 시간입니다.|활성 또는 대기 중인 요청에 대 한 null 그렇지 않으면 현재 작거나 유효한 datetime입니다.|  
|total_elapsed_time|**int**|요청 시간 (밀리초)에서 시작 된 이후 실행에서 경과한 시간입니다.|0 사이의 start_time 및 end_time 간의 차이입니다. Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건이 "최대 값을 초과 했습니다." 경고 생성 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [PolyBase 동적 관리 뷰를 사용 하 여 문제 해결](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
