---
title: sys.dm_pdw_errors (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 31f94e0424cbeafac484320adb86b0f5b6849b10
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwerrors-transact-sql"></a>sys.dm_pdw_errors (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  요청 또는 쿼리를 실행 하는 동안 발생 한 모든 오류에 대 한 정보를 보유 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|이 보기에 대 한 키입니다.<br /><br /> 오류와 관련 된 고유 숫자 id입니다.|시스템의 모든 쿼리 오류 전체에서 고유 합니다.|  
|원본(source)|**nvarchar(64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|유형|**nvarchar(4000)**|발생한 오류의 유형입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|오류가 발생 한 시간입니다.|보다 작거나 현재 시간입니다.|  
|pwd_node_id|**int**|있는 경우 관련 된 특정 노드의 식별자입니다. 노드 id에 대 한 자세한 내용은 참조 하십시오. [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.||  
|session_id|**nvarchar(32)**|있는 경우 관련 된 세션의 식별자입니다. 세션 id에 대 한 자세한 내용은 참조 하십시오. [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)합니다.||  
|request_id|**nvarchar(32)**|있는 경우 관련 된 요청의 식별자입니다. 요청 id에 대 한 자세한 내용은 참조 하십시오. [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.||  
|spid|**int**|있는 경우 관련 된 SQL Server 세션의 spid입니다.||  
|thread_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|자세히|**nvarchar(4000)**|전체 오류 텍스트 설명을 포함 합니다.||  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에 최대 시스템 뷰의 값 섹션을 참조는 [최소값 및 최 댓 값 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) 항목입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
