---
title: CLOSE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE_TSQL
- CLOSE
dev_langs: TSQL
helpviewer_keywords:
- closing cursors
- cursors [SQL Server], closing
- CLOSE statement
ms.assetid: 21546874-97e3-4b93-970f-87c27f6b78c7
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 35db1dd308c9c86c5425cedc89a75b67246f9bf5
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="close-transact-sql"></a>CLOSE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 결과 집합을 해제하고 커서가 위치한 행에 보유된 커서 잠금을 해제하여 열린 커서를 닫습니다. CLOSE는 데이터 구조를 다시 열 수 있도록 방치하지만 커서를 다시 열 때까지 인출과 위치 지정 업데이트는 허용되지 않습니다. CLOSE는 열려 있는 커서에만 실행할 수 있으며 선언만 되었거나 이미 닫혀 있는 커서에는 사용할 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CLOSE { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>인수  
 GLOBAL  
 지정 하는 *cursor_name* 전역 커서를 참조 합니다.  
  
 *cursor_name*  
 열린 커서의 이름입니다. 전역와 로컬 커서가 있는 경우 *cursor_name* 해당 이름으로 *cursor_name* GLOBAL이 고, 그렇지 않으면 지정 된 경우 전역 커서를 말합니다 *cursor_name* 로컬 커서를 참조 합니다.  
  
 *cursor_variable_name*  
 열린 커서와 연관된 커서 변수의 이름입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 커서 기반 프로세스에서 `CLOSE` 문의 정확한 위치를 보여 줍니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [커서](../../relational-databases/cursors.md)   
 [커서&#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [할당 해제 &#40; Transact SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40; Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [열기 &#40; Transact SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
