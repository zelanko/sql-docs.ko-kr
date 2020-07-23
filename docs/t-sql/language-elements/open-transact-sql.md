---
title: OPEN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPEN_TSQL
- OPEN
dev_langs:
- TSQL
helpviewer_keywords:
- opening cursors
- cursors [SQL Server], opening
- populating cursors [SQL Server]
- OPEN statement
- Transact-SQL cursors, opening
ms.assetid: fd1c5e3b-6045-4a42-b646-3fca76e874c1
author: rothja
ms.author: jroth
ms.openlocfilehash: 73199a9dba314f845c8dbb4268da0cc4fd0f4af4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919917"
---
# <a name="open-transact-sql"></a>OPEN(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  DECLARE CURSOR 또는 SET [!INCLUDE[tsql](../../includes/tsql-md.md)]cursor_variable[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 지정된 *문을 실행하여* 서버 커서를 열고 커서를 채웁니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
OPEN { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 GLOBAL  
 *cursor_name*이 전역 커서를 참조하도록 지정합니다.  
  
 *cursor_name*  
 선언된 커서의 이름입니다. 동일한 *cursor_name*을 가진 전역 커서와 지역 커서가 있을 경우 GLOBAL이 지정되면 *cursor_name*은 전역 커서를 참조하고 GLOBAL이 지정되지 않으면 *cursor_name*은 지역 커서를 참조합니다.  
  
 *cursor_variable_name*  
 커서를 나타내는 커서 변수의 이름입니다.  
  
## <a name="remarks"></a>설명  
 INSENSITIVE 또는 STATIC 옵션을 사용하여 커서를 선언한 경우 OPEN은 임시 테이블을 만들어 결과 집합을 보관합니다. 결과 집합에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 최대 행 크기를 초과하는 행이 있으면 OPEN이 실패합니다. KEYSET 옵션을 사용하여 커서를 선언하는 경우에는 OPEN이 임시 테이블을 만들어 키 집합을 보관합니다. 임시 테이블은 tempdb에 저장됩니다.  
  
 커서가 열린 후 @@CURSOR_ROWS 함수를 사용하여 마지막으로 열린 커서에서 한정하는 행 수를 받습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 키 집합 커서 또는 정적 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서를 비동기식으로 생성할 수 없습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서 작업은 일괄 처리되므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서를 비동기식으로 생성하지 않아도 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 각 커서 작업의 클라이언트 왕복 때문에 짧은 대기 시간 OPEN이 문제가 되는 비동기 키 집합 기반 또는 정적 API(애플리케이션 프로그래밍 인터페이스) 서버 커서를 계속 지원합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 커서를 열고 모든 행을 인출합니다.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN Employee_Cursor;  
  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM Employee_Cursor  
END;  
  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [@@CURSOR_ROWS&#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
