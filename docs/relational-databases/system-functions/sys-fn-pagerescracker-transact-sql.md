---
title: sys.fn_PageResCracker (TRANSACT-SQL) | Microsoft Docs
description: Sys.fn_PageResCracker 시스템 함수에 대 한 설명서입니다.
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
ms.openlocfilehash: 2fc7136b60dba47813b9942316ee6fdfbc64f307
ms.sourcegitcommit: fc1739be9b2735b2bb469979936e76ca2a3830f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58899709"
---
# <a name="sysfnpagerescracker-transact-sql"></a>sys.fn_PageResCracker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

반환 된 `db_id`, `file_id`, 및 `page_id` 에 대 한는 지정 `page_resource` 값. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>인수  
*page_resource*    
데이터베이스 페이지 리소스의 8 바이트 16 진수 형식이입니다.
  
## <a name="tables-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|db_id|**ssNoversion**|데이터베이스 ID|  
|file_id|**ssNoversion**|파일 ID|  
|page_id|**ssNoversion**|페이지 ID|  
  
## <a name="remarks"></a>Remarks  
`sys.fn_PageResCracker` 데이터베이스 ID, 파일 ID 및 페이지의 페이지 ID를 포함 하는 행 집합 데이터베이스 페이지의 8 바이트 16 진수 표현으로 변환 됩니다.   

올바른 페이지 리소스를 가져올 수 있습니다는 `page_resource` 의 열을 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 동적 관리 뷰 또는 [sys.sysprocesses &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) 시스템 뷰. 잘못 된 페이지 리소스를 사용 하는 경우 반환은 NULL입니다.  
주된 용도 `sys.fn_PageResCracker` 은 이러한 보기 간 조인이 용이 하도록 및 [sys.dm_db_page_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) 와 같은 페이지에 대 한 정보를 얻기 위해 동적 관리 함수는 속해 있는 개체입니다.
  
## <a name="permissions"></a>사용 권한  
사용자가 필요한 `VIEW SERVER STATE` 서버에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
합니다 `sys.fn_PageResCracker` 함수를 함께에서 사용할 수 있습니다 [sys.dm_db_page_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) 페이지의 문제를 해결 하려면 관련 대기 및에서 차단 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  다음 스크립트는 이러한 함수를 사용 하 여 현재 페이지 리소스의 일부 형식에 대기 중인 모든 활성 요청에 대 한 데이터베이스 페이지 정보를 수집 하는 방법의 예입니다. 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sys.sysprocesses&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
