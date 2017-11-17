---
title: "세션 ID (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
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
ms.assetid: 2a0d500a-f6c8-490f-9abd-3ae824986404
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9089c21109d6eedb1cdae0082e1530e8d77d9dde
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="sessionid-transact-sql"></a>세션 ID (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  현재 ID를 반환 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] 세션입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **nvarchar (32)** 값입니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 세션 ID 연결 되는 경우 각 사용자 연결에 할당 됩니다. 연결 기간 동안 유지 됩니다. 연결이 끝나면 세션 ID가 해제 됩니다.  
  
 세션 ID는 알파벳 문자 'SID'로 시작합니다. 이들 대/소문자 구분 되며에 세션 ID를 사용 하는 대문자로 시작 해야 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 명령입니다.  
  
 뷰를 쿼리하여 수 [sys.dm_pdw_exec_sessions](http://msdn.microsoft.com/en-us/5b656c55-427f-4306-8bd9-9d7987c203d9) 이 함수와 동일한 정보를 검색 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 세션 ID를 반환합니다.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DB_NAME &#40; Transact SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [버전 &#40; SQL 데이터 웨어하우스 &#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  

