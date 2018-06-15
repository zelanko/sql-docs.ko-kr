---
title: sys.dm_exec_compute_node_status (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODE_STATUS_TSQL
- DM_EXEC_COMPUTE_NODE_STATUS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_compute_node_status
- sys.dm_exec_compute_node_status management view
ms.assetid: b606f91f-3a08-4a4f-bb57-32ae155b3738
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 79f0c7a7596f04f768a0ec4398ec90800bbbd08e
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464179"
---
# <a name="sysdmexeccomputenodestatus-transact-sql"></a>sys.dm_exec_compute_node_status (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  성능 및 상태는 모든 노드의 PolyBase에 대 한 추가 정보를 보유합니다. 노드당 한 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.|형식에 관계 없이 스케일 아웃 클러스터 전체에서 고유 합니다.|  
|process_id|**int**|||  
|process_name|**nvarchar(255)**|노드의 논리적 이름입니다.|적절 한 길이의 문자열입니다.|  
|allocated_memory|**bigint**|Total이 노드에서 메모리를 할당 합니다.||  
|available_memory|**bigint**|이 노드의 총 사용 가능한 메모리를 지원 합니다.||  
|process_cpu_usage|**bigint**|눈금에서의 총 프로세스 CPU 사용량||  
|total_cpu_usage|**bigint**|총 CPU 사용량, 틱에서입니다.||  
|thread_count|**bigint**|이 노드에서 사용 중인 스레드의 총 수입니다.||  
|handle_count|**bigint**|이 노드에서 사용 중인 핸들의 총 수입니다.||  
|total_elapsed_time|**bigint**|시스템 시작 또는 다시 시작 이후 경과 하는 총 시간입니다.|시스템 시작 또는 다시 시작 이후 경과 하는 총 시간입니다. Total_elapsed_time 정수 (밀리초에서 24.8 일)에 대 한 최대값을 초과 하면 오버플로 materialization 오류로 인해 발생 합니다. 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
|is_available|**bit**|이 노드를 사용할 수 있는지 여부를 나타내는 플래그입니다.||  
|sent_time|**datetime**|이 네트워크 패키지를 보낸 마지막 시간||  
|received_time|**datetime**|마지막으로이 노드에서 네트워크 패키지를 보냈습니다.||  
|error_id|**nvarchar(36)**|이 노드에서 발생 한 마지막 오류의 고유 식별자입니다.||  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 동적 관리 뷰를 사용한 문제 해결](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
