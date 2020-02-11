---
title: sys. dm_pdw_os_threads (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ddc12f05-edeb-4848-b6d7-e851684cf044
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a4b9028d30db3c36157ef3db628dcb7c1cbeda00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899223"
---
# <a name="sysdm_pdw_os_threads-transact-sql"></a>sys. dm_pdw_os_threads (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|영향을 받는 노드의 ID입니다.<br /><br /> pdw_node_id 및 thread_id이 보기의 키를 구성 합니다.|[Dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)에서 node_id를 참조 하세요.|  
|thread_id|**int**|pdw_node_id 및 thread_id이 보기의 키를 구성 합니다.||  
|process_id|**int**|||  
|name|**nvarchar(255)**|||  
|우선 순위|**int**|||  
|start_time|**datetime**|||  
|state|**nvarchar (32)**|||  
|wait_reason|**nvarchar (32)**|||  
|total_processor_elapsed_time|**bigint**|스레드에서 사용 하는 총 커널 시간입니다.||  
|total_user_elapsed_time|**bigint**|스레드에서 사용 하는 총 사용자 시간||  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
