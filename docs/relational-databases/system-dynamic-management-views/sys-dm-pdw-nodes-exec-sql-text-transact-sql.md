---
title: sys.dm_pdw_nodes_exec_sql_text (Transact-sql) | Microsoft Docs
description: 지정 된 sql_handle으로 식별 되는 SQL 일괄 처리의 텍스트를 반환 하는 동적 관리 뷰입니다.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 2bf5b58a1e9dca5f282691ae29dd534a06ca5002
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92059479"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>sys.pdw_nodes_dm_exec_sql_text (Transact-sql)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

지정 된 *sql_handle*에 의해 식별 되는 SQL 일괄 처리의 텍스트를 반환 합니다. 이 테이블 반환 함수는 시스템 함수 **fn_get_sql**을 대체합니다.  
   
## <a name="table-returned"></a>반환 된 테이블  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|노드와 연결 된 고유 숫자 ID입니다.|
|**dbid**|**smallint**|데이터베이스의 ID입니다.<br /><br /> 계획 되지 않은 SQL 문 및 준비 된 SQL 문의 경우 문이 컴파일된 데이터베이스의 ID입니다.|  
|**objectid**|**int**|개체의 ID입니다.<br /><br /> 임시 및 준비된 SQL 문의 경우 NULL입니다.|  
|**number**|**smallint**|번호가 있는 저장 프로시저의 경우 저장 프로시저의 번호가 이 열에 반환됩니다. 자세한 내용은 [sys.numbered_procedures &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)를 참조 하세요.<br /><br /> 임시 및 준비된 SQL 문의 경우 NULL입니다.|  
|**됨**|**bit**|1: SQL 텍스트가 암호화 됩니다.<br /><br /> 0: SQL 텍스트가 암호화 되지 않습니다.|  
|**text**|**nvarchar(max)**|SQL 쿼리의 텍스트입니다.<br /><br /> 암호화된 개체의 경우 NULL입니다.|  

## <a name="remarks"></a>설명  
[Sys.dm_exec_sql_text](./sys-dm-exec-sql-text-transact-sql.md?view=sql-server-ver15) 에 동일한 설명이 적용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대 한 **sysadmin** 서버 역할 또는 `VIEW SERVER STATE` 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>다음 단계
 더 많은 개발 팁은 [Azure Synapse Analytics 개발 개요](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)를 참조 하세요.