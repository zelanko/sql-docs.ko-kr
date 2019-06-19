---
title: '@@FETCH_STATUS(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@FETCH_STATUS'
- '@@FETCH_STATUS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- status information [SQL Server], FETCH
- '@@FETCH_STATUS function'
ms.assetid: 93659193-e4ff-4dfb-9043-0c4114921b91
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b913dc4de858bb8d8bd70cccbd6ed9b7c4143174
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65946088"
---
# <a name="x40x40fetchstatus-transact-sql"></a>&#x40;&#x40;FETCH_STATUS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 현재 연결에서 연 모든 커서에 실행된 마지막 커서 FETCH 문의 상태를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>반환 형식  
 **integer**  
  
## <a name="return-value"></a>반환 값  
  
|반환 값|설명|  
|------------------|-----------------|  
|&nbsp;0|FETCH 문이 성공적으로 수행되었습니다.|  
|-1|FETCH 문이 실패했거나 행이 결과 집합의 범위를 벗어났습니다.|  
|-2|인출된 행이 없습니다.|
|-9|커서는 페치 작업을 수행하지 않습니다.|  
  
## <a name="remarks"></a>Remarks  
`@@FETCH_STATUS`는 연결의 모든 커서에 전역으로 적용되므로 신중히 사용하세요. FETCH 문이 실행된 후 다른 커서에 대해 다른 FETCH 문을 실행하기 전에 `@@FETCH_STATUS`의 테스트를 수행해야 합니다. `@@FETCH_STATUS`는 연결에서 페치가 수행되기 전에 정의되지 않습니다.  
  
예를 들어 사용자는 한 커서에서 FETCH 문을 실행한 후 다른 커서에서 결과를 열고 처리하는 저장 프로시저를 호출합니다. 호출된 저장 프로시저에서 컨트롤이 반환되면 `@@FETCH_STATUS`는 저장 프로시저 내에서 실행된 마지막 FETCH를 반영하고 저장 프로시저가 호출되기 전에 실행된 FETCH 문은 반영하지 않습니다.  
  
특정 커서의 마지막 페치 상태를 검색하려면 **sys.dm_exec_cursors** 동적 관리 함수의 **fetch_status** 열을 쿼리하세요.  
  
## <a name="examples"></a>예  
다음 예에서는 `@@FETCH_STATUS`를 사용하여 `WHILE` 루프에서 커서 작업을 제어합니다.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT BusinessEntityID, JobTitle  
FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [커서 함수&#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
