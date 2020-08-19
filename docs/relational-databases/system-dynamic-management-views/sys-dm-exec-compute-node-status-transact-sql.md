---
description: sys. dm_exec_compute_node_status (Transact-sql)
title: sys. dm_exec_compute_node_status (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 182a6fff7ff2cf0af1b009a3c5acc79e00c8365a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447634"
---
# <a name="sysdm_exec_compute_node_status-transact-sql"></a>sys. dm_exec_compute_node_status (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  모든 PolyBase 노드의 성능 및 상태에 대 한 추가 정보를 포함 합니다. 노드당 하나의 행을 나열 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|`int`|노드와 연결 된 고유 숫자 id입니다.|형식에 관계 없이 스케일 아웃 클러스터에서 고유 합니다.|  
|process_id|`int`|||  
|process_name|`nvarchar(255)`|노드의 논리적 이름입니다.|적절 한 길이의 문자열입니다.|  
|allocated_memory|`bigint`|이 노드에 할당 된 총 메모리입니다.||  
|available_memory|`bigint`|이 노드에서 사용할 수 있는 총 메모리입니다.||  
|process_cpu_usage|`bigint`|총 프로세스 CPU 사용량 (틱)입니다.||  
|total_cpu_usage|`bigint`|총 CPU 사용량 (틱)입니다.||  
|thread_count|`bigint`|이 노드에서 사용 중인 총 스레드 수입니다.||  
|handle_count|`bigint`|이 노드에서 사용 중인 총 핸들 수입니다.||  
|total_elapsed_time|`bigint`|시스템을 시작 하거나 다시 시작한 이후 경과 된 총 시간입니다.|시스템을 시작 하거나 다시 시작한 이후 경과 된 총 시간입니다. Total_elapsed_time 정수 24.8 (밀리초)의 최대값을 초과 하는 경우 오버플로로 인 한 구체화 실패가 발생 합니다. 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
|is_available|`bit`|이 노드를 사용할 수 있는지 여부를 나타내는 플래그입니다.||  
|sent_time|`datetime`|네트워크 패키지가 마지막으로 전송 된 시간||  
|received_time|`datetime`|이 노드에서 네트워크 패키지를 마지막으로 보낸 시간입니다.||  
|error_id|`nvarchar(36)`|이 노드에서 발생 한 마지막 오류의 고유 식별자입니다.||
|compute_pool_id|`int`|풀에 대 한 고유 식별자입니다.|

## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰를 사용한 PolyBase 문제 해결](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
