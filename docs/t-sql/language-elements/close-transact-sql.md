---
title: CLOSE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLOSE_TSQL
- CLOSE
dev_langs:
- TSQL
helpviewer_keywords:
- closing cursors
- cursors [SQL Server], closing
- CLOSE statement
ms.assetid: 21546874-97e3-4b93-970f-87c27f6b78c7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4c98cff1909bc74ff550ea9d68359d7a845d04d7
ms.sourcegitcommit: f1cf91e679d1121d7f1ef66717b173c22430cb42
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2018
ms.locfileid: "52586236"
---
# <a name="close-transact-sql"></a>CLOSE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 결과 집합을 해제하고 커서가 위치한 행에 보유된 커서 잠금을 해제하여 열린 커서를 닫습니다. `CLOSE`는 데이터 구조를 다시 열도록 내버려두지만 커서를 다시 열 때까지 인출과 위치 지정 업데이트는 허용되지 않습니다. CLOSE는 열려 있는 커서에서만 실행되어야 하며 `CLOSE`는 선언만 되었거나 이미 닫혀 있는 커서에서는 사용할 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CLOSE { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>인수  
 GLOBAL  
 *cursor_name*이 전역 커서를 참조하도록 지정합니다.  
  
 *cursor_name*  
 열린 커서의 이름입니다. 동일한 *cursor_name*을 가진 전역 커서와 지역 커서가 있을 경우 GLOBAL이 지정되면 *cursor_name*은 전역 커서를 참조하고 GLOBAL이 지정되지 않으면 *cursor_name*은 지역 커서를 참조합니다.  
  
 *cursor_variable_name*  
 열린 커서와 연관된 커서 변수의 이름입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 커서 기반 프로세스에서 `CLOSE` 문의 정확한 위치를 보여 줍니다.  
  
```sql  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title FROM AdventureWorks2012.HumanResources.Employee;  
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
 [커서](../../relational-databases/cursors.md)   
 [커서&#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN&#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
