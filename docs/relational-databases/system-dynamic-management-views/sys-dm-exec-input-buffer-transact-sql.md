---
title: sys.dm_exec_input_buffer (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c22a13e5bbb9aa8d742272515ae9fd882623596d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecinputbuffer-transact-sql"></a>sys.dm_exec_input_buffer (Transact SQL)
[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

  인스턴스에 제출 된 문에 대 한 정보를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```  
sys.dm_exec_input_buffer ( session_id , request_id )
```  
  
## <a name="arguments"></a>인수  
*session_id*  
세션 id를 조회할 수로 일괄 처리를 중입니다. *session_id* 은 **smallint**합니다. *session_id* 다음 동적 관리 개체에서 가져올 수 있습니다.  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)   
  
*request_id*  
request_id [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)합니다. *request_id* 은 **int**합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**event_type**|**nvarchar(256)**|지정 된 spid에 대 한 입력된 버퍼에서 이벤트의 형식입니다.|  
|**parameters**|**smallint**|제공 된 문에 대 한 모든 매개 변수입니다.|  
|**event_info**|**nvarchar(max)**|지정 된 spid에 대 한 입력된 버퍼에 있는 문의 텍스트입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 사용자에 게 VIEW SERVER STATE 권한이 있으면 나타납니다 실행 중인 모든 세션의 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 그렇지 않으면 현재 세션에만 표시 됩니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 데이터베이스 소유자 인 경우 사용자에 실행 중인 모든 세션을 표시 됩니다는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 그렇지 않으면 현재 세션에만 표시 됩니다.  
  
## <a name="remarks"></a>주의  
 수행 하 여 sys.dm_exec_sessions 또는 sys.dm_exec_requests와 함께에서이 동적 관리 함수를 사용할 수 있습니다 **CROSS APPLY**합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example"></a>1. 간단한 예  
 다음 예제에서는 함수에는 세션 id (SPID)와 요청 id를 전달 하는 방법을 보여 줍니다.  
  
```sql  
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```  
  
### <a name="b-using-cross-apply-to-additional-information"></a>2. 크로스 사용 하 여 추가 정보에 적용  
 다음 예제에서는 세션 id가 50 보다 크므로 인 세션에 대 한 입력된 버퍼를 나열합니다.  
  
```sql  
SELECT es.session_id, ib.event_info   
FROM sys.dm_exec_sessions AS es  
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib  
WHERE es.session_id > 50;
GO
```  
  
## <a name="see-also"></a>관련 항목:  
 [실행 관련 동적 관리 뷰 및 함수 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [DBCC INPUTBUFFER&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
