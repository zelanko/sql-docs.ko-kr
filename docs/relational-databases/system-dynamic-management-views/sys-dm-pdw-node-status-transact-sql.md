---
title: sys.dm_pdw_node_status (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 423bae3ce66e21721e328a23d51a8356be40ea2a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38000805"
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>sys.dm_pdw_node_status (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  추가 정보를 보관 (위에 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) 성능 및 모든 어플라이언스 노드의 상태에 대 한 합니다. 어플라이언스의 노드 당 하나의 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기에 대 한 키입니다.|형식에 관계 없이 어플라이언스에서 고유 합니다.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|이 노드에서 메모리를 할당 된 총 수입니다.||  
|available_memory|**bigint**|이 노드의 총 사용 가능한 메모리를 지원 합니다.||  
|process_cpu_usage|**bigint**|총 프로세스 CPU 사용량, 틱입니다.||  
|total_cpu_usage|**bigint**|총 CPU 사용량, 틱입니다.||  
|thread_count|**bigint**|이 노드에서 사용 중인 스레드의 총 수입니다.||  
|handle_count|**bigint**|이 노드에서 사용 중인 핸들의 총 수입니다.||  
|total_elapsed_time|**bigint**|시스템 시작 되거나 다시 시작 이후 경과 된 총 시간입니다.|시스템 시작 되거나 다시 시작 이후 경과 된 총 시간입니다. Total_elapsed_time 정수 (밀리초 단위로 24.8 일)에 대 한 최대값을 초과 하는 경우 materialization 오류로 인해 오버플로를 발생 합니다.<br /><br /> 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
|is_available|**bit**|이 노드를 사용할 수 있는지 여부를 나타내는 플래그입니다.||  
|sent_time|**datetime**|이 노드가 네트워크 패키지를 보낸 최종 시간입니다.||  
|received_time|**datetime**|네트워크 패키지를이 노드에 의해 수신 된 마지막 시간입니다.||  
|error_id|**nvarchar(36)**|이 노드에서 발생 한 마지막 오류의 고유 식별자입니다.||  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
