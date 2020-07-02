---
title: sys. fn_PageResCracker (Transact-sql) | Microsoft Docs
description: Sys. fn_PageResCracker 시스템 함수에 대 한 설명서입니다.
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_PageResCracker
- sys.fn_PageResCracker_TSQL
- fn_PageResCracker_TSQL
- sys.fn_PageResCracker
- sys.dm_db_page_info
dev_langs:
- TSQL
helpviewer_keywords:
- fn_PageResCracker function
- page_resource
- sys.fn_PageResCracker function
- sys.dm_db_page_info
- page info
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: 460f1990a7020d7a57ea7ad543f3253576756d05
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790432"
---
# <a name="sysfn_pagerescracker-transact-sql"></a>sys. fn_PageResCracker (Transact-sql)
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

`db_id` `file_id` `page_id` 지정 된 값에 대해, 및를 반환 합니다 `page_resource` . 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>인수  
*page_resource*    
데이터베이스 페이지 리소스의 8 바이트 16 진수 형식입니다.
  
## <a name="tables-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|db_id|**int**|데이터베이스 ID|  
|file_id|**int**|파일 ID|  
|page_id|**int**|페이지 ID|  
  
## <a name="remarks"></a>설명  
`sys.fn_PageResCracker`는 데이터베이스 페이지의 8 바이트 16 진수 표현을 해당 페이지의 데이터베이스 ID, 파일 ID 및 페이지 ID를 포함 하는 행 집합으로 변환 하는 데 사용 됩니다.   

`page_resource` [Dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 동적 관리 뷰 또는 [transact-sql &#40;시스템&#41;sys.sys프로세스](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) 의 열에서 유효한 페이지 리소스를 가져올 수 있습니다. 잘못 된 페이지 리소스를 사용 하는 경우에는 NULL이 반환 됩니다.  
의 주요 용도는 `sys.fn_PageResCracker` 이러한 뷰와 [Dm_db_page_info &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) 동적 관리 함수 간의 조인을 용이 하 게 하는 것입니다 .이 함수는 페이지에 대 한 정보 (예: 자신이 속한 개체)를 가져오기 위해 사용 됩니다.
  
## <a name="permissions"></a>사용 권한  
사용자에 게 `VIEW SERVER STATE` 서버에 대 한 권한이 필요 합니다.  
  
## <a name="examples"></a>예제  
`sys.fn_PageResCracker`함수는 [Dm_db_page_info &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) 와 함께 사용 하 여 페이지 관련 대기 및 블로킹 문제를 해결할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  다음 스크립트는 이러한 함수를 사용 하 여 현재 특정 유형의 페이지 리소스에서 대기 중인 모든 활성 요청에 대 한 데이터베이스 페이지 정보를 수집 하는 방법의 예입니다. 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>참고 항목  
 [dm_db_page_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [Transact-sql&#41;&#40;프로세스sys.sys](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests&#40;Transact-SQL&#41](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
