---
title: SESSION_ID(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/23/2018
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fbc453282e442e9adb5a378c216b2e5a83eb2bb0
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/24/2018
---
# <a name="sessionid-transact-sql"></a>SESSION_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  현재 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] 세션의 ID를 반환합니다.  
  
 ![토픽 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "토픽 링크 아이콘")[Transact-SQL 구문 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>반환 값  
 **nvarchar(32)** 값을 반환합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 세션 ID는 연결할 때 각 사용자 연결에 할당되며 연결 기간 동안 유지됩니다. 연결이 종료되면 세션 ID가 해제됩니다.  
  
 세션 ID는 알파벳 문자 'SID'로 시작합니다. 이는 대/소문자를 구분하며 세션 ID가 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 명령에 사용될 때 대문자로 바뀝니다.  
  
 [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 뷰를 쿼리하여 이 기능과 같은 정보를 검색할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 현재 세션 ID를 반환합니다.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>참고 항목  
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40;SQL Data Warehouse&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
