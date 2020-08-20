---
description: sys. dm_pdw_errors (Transact-sql)
title: sys. dm_pdw_errors (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 9dbc33260f68a6258373ed77cca32835a1906dd1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474781"
---
# <a name="sysdm_pdw_errors-transact-sql"></a>sys. dm_pdw_errors (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  요청 또는 쿼리를 실행 하는 동안 발생 한 모든 오류에 대 한 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar (36)**|이 보기의 키입니다.<br /><br /> 오류와 연결 된 고유 숫자 id입니다.|시스템의 모든 쿼리 오류에서 고유 합니다.|  
|source|**nvarchar (64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|type|**nvarchar(4000)**|발생한 오류의 유형입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|오류가 발생 한 시간입니다.|현재 시간 보다 작거나 같습니다.|  
|pwd_node_id|**int**|관련 된 특정 노드의 식별자입니다 (있는 경우). 노드 id에 대 한 자세한 내용은 [dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)을 참조 하십시오.||  
|session_id|**nvarchar(32)**|관련 된 세션의 식별자입니다 (있는 경우). 세션 id에 대 한 자세한 내용은  [dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)을 참조 하십시오.||  
|request_id|**nvarchar(32)**|관련 된 요청에 대 한 식별자입니다 (있는 경우). 요청 id에 대 한 자세한 내용은 [dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)을 참조 하십시오.||  
|spid|**int**|관련 된 SQL Server 세션의 spid입니다 (있는 경우).||  
|thread_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|자세히|**nvarchar(4000)**|전체 오류 텍스트 설명을 저장 합니다.||  
  
 이 보기에 의해 유지 되는 최대 행에 대 한 자세한 내용은 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목에서 메타 데이터 섹션을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
