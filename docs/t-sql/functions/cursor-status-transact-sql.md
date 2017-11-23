---
title: CURSOR_STATUS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURSOR_STATUS
- CURSOR_STATUS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- status information [SQL Server], cursors
- CURSOR_STATUS function
- cursors [SQL Server], status information
ms.assetid: 3a4a840e-04f8-43bd-aada-35d78c3cb6b0
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 59a2cd382855f47d7cb37a3bc00bc723dde8f6df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="cursorstatus-transact-sql"></a>CURSOR_STATUS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

프로시저가 지정된 매개 변수에 대한 커서 및 결과 집합을 반환하는지 여부를 저장 프로시저 호출자가 확인할 수 있도록 하는 스칼라 함수입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CURSOR_STATUS   
     (  
          { 'local' , 'cursor_name' }   
          | { 'global' , 'cursor_name' }   
          | { 'variable' , 'cursor_variable' }   
     )  
```  
  
## <a name="arguments"></a>인수  
'local'  
커서의 원본이 로컬 커서 이름임을 나타내는 상수입니다.
  
'*cursor_name*'  
커서의 이름입니다. 커서 이름은 식별자에 대한 규칙을 따라야 합니다.
  
'global'  
커서의 원본이 전역 커서 이름임을 나타내는 상수입니다.
  
'variable'  
커서의 원본이 지역 변수임을 나타내는 상수입니다.
  
'*cursor_variable*'  
커서 변수의 이름입니다. 커서 변수를 사용 하 여 정의 해야 합니다는 **커서** 데이터 형식입니다.
  
## <a name="return-types"></a>반환 형식
**smallint**
  
|반환 값|커서 이름|커서 변수|  
|---|---|---|
|1.|커서의 결과 집합에 최소 한 개의 행이 있습니다.<br /><br /> 변경 감지 불능 커서와 키 집합 커서의 경우 결과 집합에 최소 한 개의 행이 있습니다.<br /><br /> 동적 커서의 경우 결과 집합에는 0개, 1개 또는 그 이상의 행이 있습니다.|이 변수에 할당된 커서가 열려 있습니다.<br /><br /> 변경 감지 불능 커서와 키 집합 커서의 경우 결과 집합에 최소 한 개의 행이 있습니다.<br /><br /> 동적 커서의 경우 결과 집합에는 0개, 1개 또는 그 이상의 행이 있습니다.|  
|0|커서의 결과 집합이 비어 있습니다.*|이 변수에 할당된 커서는 열려 있지만 결과 집합은 확실히 비어 있습니다.*|  
|-1|커서가 닫혀 있습니다.|이 변수에 할당된 커서가 닫혀 있습니다.|  
|-2|이 오류에는 이 작업을 적용할 수 없습니다.|다음 값 중 하나일 수 있습니다.<br /><br /> 이전에 호출된 프로시저에서 이 OUTPUT 변수에 할당한 커서가 없습니다.<br /><br /> 이전에 호출된 프로시저에서 이 OUTPUT 변수로 커서가 할당되었지만 프로시저가 완료되면서 닫혔습니다. 따라서 커서는 할당 취소되고 호출하는 프로시저로 반환되지 않습니다.<br /><br /> 선언된 커서 변수에 할당된 커서가 없습니다.|  
|-3|지정된 이름의 커서가 없습니다.|지정된 이름의 커서 변수가 없거나 있는 경우에는 아직 커서가 할당되지 않았습니다.|  
  
*동적 커서는 절대 이 결과를 반환하지 않습니다.
  
## <a name="examples"></a>예  
다음 예에서는 `CURSOR_STATUS` 함수를 사용하여 커서를 열고 닫기 전후의 커서 상태를 표시합니다.
  
```sql
CREATE TABLE #TMP  
(  
   ii int  
)  
GO  
  
INSERT INTO #TMP(ii) VALUES(1)  
INSERT INTO #TMP(ii) VALUES(2)  
INSERT INTO #TMP(ii) VALUES(3)  
  
GO  
  
--Create a cursor.  
DECLARE cur CURSOR  
FOR SELECT * FROM #TMP  
  
--Display the status of the cursor before and after opening  
--closing the cursor.  
  
SELECT CURSOR_STATUS('global','cur') AS 'After declare'  
OPEN cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Open'  
CLOSE cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Close'  
  
--Remove the cursor.  
DEALLOCATE cur  
  
--Drop the table.  
DROP TABLE #TMP  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
After declare
---------------
-1  
  
After Open
----------
1  
  
After Close
-----------
-1
```  
  
## <a name="see-also"></a>참고 항목
[커서 함수 &#40; Transact SQL &#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
