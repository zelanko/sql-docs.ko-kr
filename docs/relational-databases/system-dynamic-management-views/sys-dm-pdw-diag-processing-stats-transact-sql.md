---
title: sys.dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f96dd7be6de1415abb8a71425b083c58e7012d9d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023994"
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  관리자가 정의 하는 진단 세션에 통합 될 수 있는 모든 내부 진단 이벤트와 관련 된 정보를 표시 합니다. 진단 및 이벤트 하위 시스템 통계 다른 Dmv의 채우기 해당 드라이브를 이해 하려면이 뷰를 쿼리 합니다. 그룹에 각 노드에 있는 각 프로세스에 대 한 큐에 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|이 로그는 어플라이언스 노드입니다.|  
|**process_id**|**int**|이 통계를 제출 하는 실행 중인 프로세스의 식별자입니다.|  
|**target_name**|**nvarchar(255)**|큐의 이름입니다.|  
|**queue_size**|**int**|프로세스 큐에 있는 항목의 수입니다. 큐 크기는 일반적으로 0입니다. 양수 값을 나타내고 시스템은 부하가 이벤트의 백로그를 구성 하는 합니다. 다른 열에 양수는 해당 특정 큐에 대 한 손상 된 시스템 및 Dmv 관련 의미 합니다.|  
|**lost_events_count**|**bigint**|손실 되는 이벤트의 수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
