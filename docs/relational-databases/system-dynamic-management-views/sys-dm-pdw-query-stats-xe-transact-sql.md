---
description: sys.dm_pdw_query_stats_xe (Transact-sql)
title: sys.dm_pdw_query_stats_xe (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d551241-db35-4958-b60f-55e996f95c1f
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 9208823cd17c5638b759e3608280773ea60c454a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440738"
---
# <a name="sysdm_pdw_query_stats_xe-transact-sql"></a>sys.dm_pdw_query_stats_xe (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  이 DMV는 더 이상 사용 되지 않으며 이후 릴리스에서 제거 될 예정입니다. 이 릴리스에서는 0 개의 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|이벤트|**nvarchar(60)**|이 보기의 키입니다.||  
|event_id|**nvarchar (36)**|||  
|create_time|**datetime**|||  
|session_id|**int**|세션의 id입니다.|[Sys.dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)에서 session_id를 참조 하세요.|  
|cpu|**int**|||  
|reads|**int**|이벤트가 시작 된 이후의 논리적 읽기 수입니다.||  
|writes|**int**|이벤트가 시작 된 이후의 논리적 쓰기 수입니다.||  
|sql_text|**nvarchar(4000)**|||  
|client_app_name|**nvarchar(255)**|||  
|tsql_stack|**nvarchar(255)**|||  
|pdw_node_id|**int**|이 Xevent 인스턴스가 실행 되는 노드입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
