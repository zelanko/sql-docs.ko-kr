---
title: '@@FETCH_STATUS (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 61e209f7cf2a3a654b33979129e9500d3734fe64
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40fetchstatus-transact-sql"></a>& #x 40; & #x 40; FETCH_STATUS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 연결에서 연 모든 커서에 대해 실행된 마지막 커서 FETCH 문의 상태를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>반환 형식  
 **integer**  
  
## <a name="return-value"></a>반환 값  
  
|반환 값|Description|  
|------------------|-----------------|  
|0|FETCH 문이 성공적으로 수행되었습니다.|  
|-1|FETCH 문이 실패했거나 행이 결과 집합의 범위를 벗어났습니다.|  
|-2|인출된 행이 없습니다.|
|-9|커서는 인출 작업을 수행 하지 않습니다.|  
  
## <a name="remarks"></a>주의  
 때문에 @@FETCH_STATUS 는 전체 연결에 대 한 모든 커서에을 사용 하 여@FETCH_STATUS 신중 하 게 합니다. FETCH 문이 실행 된 후 @에 대 한 테스트@FETCH_STATUS 다른 커서에 대해 다른 FETCH 문을 실행 하기 전에 발생 해야 합니다. @ 값@FETCH_STATUS 연결에서 모든 인출이 수행 되기 전에 정의 되지 않습니다.  
  
 예를 들어 사용자는 한 커서에서 FETCH 문을 실행한 다음 다른 커서에서 결과를 열고 처리하는 저장 프로시저를 호출합니다. 호출된 된 저장된 프로시저에서 컨트롤이 반환 될 때@FETCH_STATUS 저장 프로시저에서 저장된 프로시저를 호출 하기 전에 실행 된 FETCH 문은 하지 실행 된 마지막 FETCH를 반영 합니다.  
  
 특정 커서의 마지막 인출 상태를 검색 하려면 쿼리는 **fetch_status** 의 열은 **sys.dm_exec_cursors** 동적 관리 함수입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [커서 함수&#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40; Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  

