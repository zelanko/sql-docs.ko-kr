---
description: sys.dm_pdw_diag_processing_stats (Transact-sql)
title: sys.dm_pdw_diag_processing_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: e050ab114773930ef3f21c3ca46381774ce0ee82
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474814"
---
# <a name="sysdm_pdw_diag_processing_stats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  관리자가 정의한 진단 세션에 통합 될 수 있는 모든 내부 진단 이벤트와 관련 된 정보를 표시 합니다. 다른 모든 Dmv의 채우기를 구동 하는 진단 및 이벤트 하위 시스템의 통계를 이해 하려면이 뷰를 쿼리 합니다. 각 노드의 각 프로세스에 대 한 큐 그룹이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|이 로그를 가져온 어플라이언스 노드입니다.|  
|**process_id**|**int**|이 통계 제출을 실행 하는 프로세스의 식별자입니다.|  
|**target_name**|**nvarchar(255)**|큐의 이름입니다.|  
|**queue_size**|**int**|프로세스 큐에 있는 항목의 수입니다. 큐 크기는 일반적으로 0입니다. 양수는 시스템이 스트레스 상태이 고 이벤트의 백로그를 작성 하 고 있음을 나타냅니다. 다른 열의 긍정 개수는 특정 큐 및 관련 Dmv에 대해 시스템이 손상 된 것을 의미 합니다.|  
|**lost_events_count**|**bigint**|손실 된 이벤트 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
