---
title: "열기 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- OPEN_TSQL
- OPEN
dev_langs: TSQL
helpviewer_keywords:
- opening cursors
- cursors [SQL Server], opening
- populating cursors [SQL Server]
- OPEN statement
- Transact-SQL cursors, opening
ms.assetid: fd1c5e3b-6045-4a42-b646-3fca76e874c1
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aec83ff9ef56b4d4ae02867d4055d0b1e38f41ec
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="open-transact-sql"></a>OPEN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  열립니다는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서를 실행 하 여 커서를 채웁니다는 [!INCLUDE[tsql](../../includes/tsql-md.md)] DECLARE CURSOR 또는 SET에 지정 된 문에 *cursor_variable* 문.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
OPEN { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>인수  
 GLOBAL  
 지정 하는 *cursor_name* 전역 커서를 참조 합니다.  
  
 *cursor_name*  
 선언된 커서의 이름입니다. 전역와 로컬 커서가 있는 경우 *cursor_name* 해당 이름으로 *cursor_name* GLOBAL이 고, 그렇지 않으면 지정 하는 경우 전역 커서를 참조 *cursor_name* 로컬 커서를 참조 합니다.  
  
 *cursor_variable_name*  
 커서를 나타내는 커서 변수의 이름입니다.  
  
## <a name="remarks"></a>주의  
 INSENSITIVE 또는 STATIC 옵션을 사용하여 커서를 선언한 경우 OPEN은 임시 테이블을 만들어 결과 집합을 보관합니다. 결과 집합에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 최대 행 크기를 초과하는 행이 있으면 OPEN이 실패합니다. KEYSET 옵션을 사용하여 커서를 선언하는 경우에는 OPEN이 임시 테이블을 만들어 키 집합을 보관합니다. 임시 테이블은 tempdb에 저장됩니다.  
  
 사용 하 여 커서를 연 후의 @@CURSOR_ROWS 마지막 열린된 커서에서 행을 한정 된 받을 함수입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 키 집합 커서 또는 정적 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서를 비동기식으로 생성할 수 없습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서 작업은 일괄 처리되므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서를 비동기식으로 생성하지 않아도 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 각 커서 작업의 클라이언트 왕복 때문에 짧은 대기 시간 OPEN이 문제가 되는 비동기 키 집합 기반 또는 정적 API(응용 프로그래밍 인터페이스) 서버 커서를 계속 지원합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [닫기 &#40; Transact SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [@@CURSOR_ROWS&#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [할당 해제 &#40; Transact SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40; Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
