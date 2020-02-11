---
title: sys. dm_pdw_query_stats_xe (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d551241-db35-4958-b60f-55e996f95c1f
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8cb9980f74bdb37b1fab43db352e35c43151c390
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899149"
---
# <a name="sysdm_pdw_query_stats_xe-transact-sql"></a>sys. dm_pdw_query_stats_xe (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  이 DMV는 더 이상 사용 되지 않으며 이후 릴리스에서 제거 될 예정입니다. 이 릴리스에서는 0 개의 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|이벤트|**nvarchar (60)**|이 보기의 키입니다.||  
|event_id|**nvarchar (36)**|||  
|create_time|**datetime**|||  
|session_id|**int**|세션의 id입니다.|[Dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)에서 session_id를 참조 하세요.|  
|cpu|**int**|||  
|reads|**int**|이벤트가 시작 된 이후의 논리적 읽기 수입니다.||  
|writes|**int**|이벤트가 시작 된 이후의 논리적 쓰기 수입니다.||  
|sql_text|**nvarchar(4000)**|||  
|client_app_name|**nvarchar(255)**|||  
|tsql_stack|**nvarchar(255)**|||  
|pdw_node_id|**int**|이 Xevent 인스턴스가 실행 되는 노드입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
