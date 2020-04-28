---
title: sys. dm_exec_compute_node_errors (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b074da717a2c5deac9d576da938d1229dafeac77
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73532787"
---
# <a name="sysdm_exec_compute_node_errors-transact-sql"></a>sys. dm_exec_compute_node_errors (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase 계산 노드에서 발생 하는 오류를 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|error_id|`nvarchar(36)`|오류와 연결 된 고유 숫자 id입니다.|시스템의 모든 쿼리 오류에서 고유|  
|source|`nvarchar(255)`|소스 스레드 또는 프로세스 설명||  
|type|`nvarchar(255)`|오류 유형입니다.||  
|create_time|`datetime`|오류가 발생 한 시간입니다.||  
|compute_node_id|`int`|특정 계산 노드의 식별자입니다.|Compute_node_id의 [dm_exec_compute_nodes &#40;transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) 을 참조 하세요&#41;|  
|rexecution_id|`nvarchar(36)`|PolyBase 쿼리 (있는 경우)의 식별자입니다.||  
|spid|`int`|SQL Server 세션의 식별자입니다.||  
|thread_id|`int`|오류가 발생 한 스레드의 숫자 식별자입니다.||  
|자세히|nvarchar(4000)|오류의 세부 정보에 대 한 전체 설명입니다.||
|compute_pool_id|`int`|풀에 대 한 고유 식별자입니다.|

  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰를 사용한 PolyBase 문제 해결](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
