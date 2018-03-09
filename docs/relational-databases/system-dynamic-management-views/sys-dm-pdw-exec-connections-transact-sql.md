---
title: sys.dm_pdw_exec_connections (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 201c0fe2d8396d5669f2a05ef43343522827c465
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwexecconnections-transact-sql"></a>sys.dm_pdw_exec_connections (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 이 인스턴스에 대해 설정된 연결에 대한 정보와 각 연결에 대한 세부 정보를 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|이 연결과 연관된 세션을 식별합니다. 사용 하 여 `SESSION_ID()` 반환 하는 `session_id` 현재 연결의 합니다.|  
|connect_time|**datetime**|연결이 설정된 타임스탬프입니다. Null을 허용하지 않습니다.|  
|encrypt_option|**nvarchar(40)**|TRUE를 나타냅니다 (연결 암호화) 또는 FALSE (연결 되지 않은 enctypred).|  
|auth_scheme|**nvarchar(40)**|이 연결에 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Windows 인증 체계를 지정합니다. Null을 허용하지 않습니다.|  
|client_id|**varchar(48)**|이 서버에 연결 하는 클라이언트의 IP 주소입니다. Null을 허용합니다.|  
|sql_spid|**int**|연결의 서버 프로세스 ID입니다. 사용 하 여 `@@SPID` 반환 하는 `sql_spid` 현재 연결의 합니다. 목적 가장을 사용 하 여는 `session_id` 대신 합니다.|  
  
## <a name="permissions"></a>Permissions  
 필요한 **VIEW SERVER STATE** 서버에 대 한 권한이 있습니다.  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
||||  
|-|-|-|  
|dm_pdw_exec_sessions.session_id|dm_pdw_exec_connections.session_id|일 대 일|  
|dm_pdw_exec_requests.connection_id|dm_pdw_exec_connections.connection_id|다 대 일|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
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
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

