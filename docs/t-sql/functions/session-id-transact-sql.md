---
description: SESSION_ID(Transact-SQL)
title: SESSION_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: VanMSFT
ms.author: vanto
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 0a3b16a5e7c5fd45f1349822afb28af4a5123557
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481884"
---
# <a name="session_id-transact-sql"></a>SESSION_ID(Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  현재 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] 세션의 ID를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
-- Azure Synapse Analytics and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>Return Value  
 **nvarchar(32)** 값을 반환합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 세션 ID는 연결할 때 각 사용자 연결에 할당되며 연결 기간 동안 유지됩니다. 연결이 종료되면 세션 ID가 해제됩니다.  
  
 세션 ID는 알파벳 문자 'SID'로 시작합니다. 이는 대/소문자를 구분하며 세션 ID가 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 명령에 사용될 때 대문자로 바뀝니다.  
  
 [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 뷰를 쿼리하여 이 기능과 같은 정보를 검색할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예제에서는 현재 세션 ID를 반환합니다.  
  
```sql  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>참고 항목  
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40;Azure Synapse Analytics&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
