---
title: sys.dm_pdw_exec_connections (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b333af29e3d39c0f4ce59ea68602f652c042003f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899414"
---
# <a name="sysdmpdwexecconnections-transact-sql"></a>sys.dm_pdw_exec_connections (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 이 인스턴스에 대해 설정된 연결에 대한 정보와 각 연결에 대한 세부 정보를 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|session_id|**int**|이 연결과 연관된 세션을 식별합니다. 사용 하 여 `SESSION_ID()` 돌아가려면는 `session_id` 현재 연결의 합니다.|  
|connect_time|**datetime**|연결이 설정된 타임스탬프입니다. Null을 허용하지 않습니다.|  
|encrypt_option|**nvarchar(40)**|TRUE 이면 (연결 암호화 됨) 또는 FALSE (연결 되지 않음 enctypred).|  
|auth_scheme|**nvarchar(40)**|이 연결에 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Windows 인증 체계를 지정합니다. Null을 허용하지 않습니다.|  
|client_id|**varchar(48)**|이 서버에 연결 하는 클라이언트의 IP 주소입니다. Null을 허용합니다.|  
|sql_spid|**int**|연결의 서버 프로세스 ID입니다. 사용 하 여 `@@SPID` 돌아가려면는 `sql_spid` 현재 연결의 합니다. 안심 가장에 사용 된 `session_id` 대신 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 필요 **VIEW SERVER STATE** 서버에 대 한 권한이 있습니다.  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
||||  
|-|-|-|  
|dm_pdw_exec_sessions.session_id|dm_pdw_exec_connections.session_id|일 대 일|  
|dm_pdw_exec_requests.connection_id|dm_pdw_exec_connections.connection_id|다 대 일|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 쿼리 자체 연결에 대한 정보를 수집하는 일반 쿼리입니다.  
  
```  
SELECT  
    c.session_id, c.encrypt_option,  
    c.auth_scheme, s.client_id, s.login_name,   
    s.status, s.query_count  
FROM sys.dm_pdw_exec_connections AS c  
JOIN sys.dm_pdw_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = SESSION_ID();  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

