---
description: sys.dm_pdw_node_status (Transact-sql)
title: sys.dm_pdw_node_status (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: ae7d516d143adb54427146a1675433575d5a2529
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461584"
---
# <a name="sysdm_pdw_node_status-transact-sql"></a>sys.dm_pdw_node_status (Transact-sql)

[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  모든 어플라이언스 노드의 성능 및 상태에 대 한 추가 정보 ( [transact-sql&#41;&#40;sys.dm_pdw_nodes ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md))를 포함 합니다. 어플라이언스의 노드당 하나의 행을 나열 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기의 키입니다.|형식에 관계 없이 어플라이언스 전체에서 고유 합니다.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|이 노드에 할당 된 총 메모리입니다.||  
|available_memory|**bigint**|이 노드에서 사용할 수 있는 총 메모리입니다.||  
|process_cpu_usage|**bigint**|총 프로세스 CPU 사용량 (틱)입니다.||  
|total_cpu_usage|**bigint**|총 CPU 사용량 (틱)입니다.||  
|thread_count|**bigint**|이 노드에서 사용 중인 총 스레드 수입니다.||  
|handle_count|**bigint**|이 노드에서 사용 중인 총 핸들 수입니다.||  
|total_elapsed_time|**bigint**|시스템을 시작 하거나 다시 시작한 이후 경과 된 총 시간입니다.|시스템을 시작 하거나 다시 시작한 이후 경과 된 총 시간입니다. Total_elapsed_time 정수 24.8 (밀리초)의 최대값을 초과 하는 경우 오버플로로 인 한 구체화 실패가 발생 합니다.<br /><br /> 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
|is_available|**bit**|이 노드를 사용할 수 있는지 여부를 나타내는 플래그입니다.||  
|sent_time|**datetime**|이 노드에서 네트워크 패키지를 마지막으로 보낸 시간입니다.||  
|received_time|**datetime**|이 노드에서 네트워크 패키지를 마지막으로 수신한 시간입니다.||  
|error_id|**nvarchar (36)**|이 노드에서 발생 한 마지막 오류의 고유 식별자입니다.||  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
