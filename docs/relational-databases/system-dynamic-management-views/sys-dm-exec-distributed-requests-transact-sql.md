---
title: sys. dm_exec_distributed_requests (Transact-sql) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 37fd17f17d8b6aa1a30f48d75258d27f4a45561a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097802"
---
# <a name="sysdm_exec_distributed_requests-transact-sql"></a>sys. dm_exec_distributed_requests (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase 쿼리에서 현재 또는 최근에 활성 상태인 모든 요청에 대 한 정보를 저장 합니다. 요청/쿼리 당 한 개의 행을 나열 합니다.  
  
 사용자는 세션 및 요청 ID에 따라 실행 되도록 생성 된 실제 분산 요청을 검색할 수 있습니다. dm_exec_distributed_requests를 통해 수행 됩니다. 예를 들어 일반 SQL 및 외부 SQL 테이블과 관련 된 쿼리는 다양 한 계산 노드에서 실행 되는 다양 한 문/요청으로 분해 됩니다. 모든 계산 노드에서 분산 단계를 추적 하기 위해 하나의 특정 요청 및 연산자와 연결 된 계산 노드의 모든 작업을 추적 하는 데 사용할 수 있는 ' 전역 ' 실행 ID를 소개 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|이 보기의 키입니다. 요청과 연결 된 고유 숫자 id입니다.|시스템의 모든 요청에 대해 고유 합니다.|  
|execution_id|**nvarchar (32**|이 쿼리가 실행 된 세션과 연결 된 고유 숫자 id입니다.||  
|상태|**nvarchar (32**|요청의 현재 상태입니다.|' Pending ', ' 권한 부여 ', ' AcquireSystemResources ', ' 초기화 중 ', ' Plan ', ' 구문 분석 ', ' AquireResources ', ' 실행 중 ', ' 취소 ', ' 완료 ', ' 실패 ', ' 취소 됨 '.|  
|error_id|**nvarchar (36)**|요청과 관련 된 오류의 고유 id입니다 (있는 경우).|오류가 발생 하지 않은 경우 NULL로 설정 합니다.|  
|start_time|**datetime**|요청 실행이 시작 된 시간입니다.|대기 중인 요청에 대해 0 그렇지 않으면 유효한 날짜/시간이 현재 시간 보다 작거나 같습니다.|  
|end_time|**datetime**|엔진이 요청 컴파일을 완료 한 시간입니다.|대기 중이거나 활성 요청의 경우 Null입니다. 그렇지 않으면 현재 시간 보다 작거나 같은 유효한 날짜/시간입니다.|  
|total_elapsed_time|**int**|요청이 시작 된 이후 실행에서 경과한 시간 (밀리초)입니다.|0과 end_time 사이의 차이를 start_time 합니다. Total_elapsed_time 정수에 대 한 최대값을 초과 하는 경우 total_elapsed_time는 최대 값으로 계속 됩니다. 이 경우 "최 댓 값이 초과 되었습니다." 라는 경고가 생성 됩니다. 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰를 사용한 PolyBase 문제 해결](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
