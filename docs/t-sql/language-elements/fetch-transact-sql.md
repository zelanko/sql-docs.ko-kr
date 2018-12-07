---
title: FETCH(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FETCH
- FETCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- cursors [SQL Server], fetching
- Transact-SQL cursors, fetching and scrolling
- retrieving rows
- fetching [SQL Server]
- SCROLL option
- row fetching [SQL Server]
ms.assetid: 5d68dac2-f91b-4342-bb4e-209ee132665f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 68d27a88ec604de05f8165f6c251982e53914794
ms.sourcegitcommit: f1cf91e679d1121d7f1ef66717b173c22430cb42
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2018
ms.locfileid: "52586216"
---
# <a name="fetch-transact-sql"></a>FETCH(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서에서 특정 행을 검색합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FETCH   
          [ [ NEXT | PRIOR | FIRST | LAST   
                    | ABSOLUTE { n | @nvar }   
                    | RELATIVE { n | @nvar }   
               ]   
               FROM   
          ]   
{ { [ GLOBAL ] cursor_name } | @cursor_variable_name }   
[ INTO @variable_name [ ,...n ] ]   
```  
  
## <a name="arguments"></a>인수  
 NEXT  
 현재 행 바로 다음의 결과 행을 반환하며 현재 행을 반환되는 행 앞의 행으로 만듭니다. 커서에 대해 `FETCH NEXT`가 첫 번째 인출인 경우 결과 집합의 첫 번째 행을 반환합니다. `NEXT`는 커서 인출의 기본 옵션입니다.  
  
 PRIOR  
 현재 행 바로 앞의 결과 행을 반환하며 현재 행을 반환되는 행 뒤의 행으로 만듭니다. 커서에 대해 `FETCH PRIOR`가 첫 번째 인출인 경우 행이 반환되지 않으며 커서는 첫 번째 행 앞에 위치하게 됩니다.  
  
 FIRST  
 커서의 첫 번째 행을 반환하며 그 행을 현재 행으로 만듭니다.  
  
 LAST  
 커서의 마지막 행을 반환하며 그 행을 현재 행으로 만듭니다.  
  
 ABSOLUTE { *n*| @*nvar*}  
 *n* 또는 @*nvar*가 양수인 경우 커서 맨 앞에서 *n*번째 행을 반환하며 반환되는 행을 새 현재 행으로 만듭니다. *n* 또는 @*nvar*가 음수인 경우에는 커서 맨 뒤에서 *n*번째 행을 반환하며 반환되는 행을 새 현재 행으로 만듭니다. *n* 또는 @*nvar*가 0이면 행이 반환되지 않습니다. *n*은 정수 상수여야 하며 @*nvar*는 **smallint**, **tinyint** 또는 **int**이어야 합니다.  
  
 RELATIVE { *n*| @*nvar*}  
 *n* 또는 @*nvar*이 양수인 경우에는 현재 행에서 위로 *n*번째 행을 반환하며 반환되는 행을 새 현재 행으로 만듭니다. *n* 또는 @*nvar*이 음수인 경우에는 현재 행에서 앞으로 *n*번째 행을 반환하며 반환되는 행을 새 현재 행으로 만듭니다. *n* 또는 @*nvar*가 0인 경우에는 현재 행을 반환합니다. *n* 또는 @*nvar*가 음수로 설정되거나 첫 번째 인출에 있는 0이 커서에 대해 수행되도록 `FETCH RELATIVE`가 지정된 경우 행은 반환되지 않습니다. *n*은 정수 상수여야 하며 @*nvar*는 **smallint**, **tinyint** 또는 **int**이어야 합니다.  
  
 GLOBAL  
 *cursor_name*이 전역 커서를 참조하도록 지정합니다.  
  
 *cursor_name*  
 인출이 수행되는 열린 커서의 이름입니다. 동일한 *cursor_name*을 가진 전역 커서와 지역 커서가 있을 경우 GLOBAL이 지정되면 *cursor_name*은 전역 커서를 참조하고 GLOBAL이 지정되지 않으면 지역 커서를 참조합니다.  
  
 @*cursor_variable_name*  
 수행할 인출에서 열린 커서를 참조하는 커서 변수의 이름입니다.  
  
 INTO @*variable_name*[ ,...*n*]  
 인출하는 열에서 지역 변수로 데이터를 가져가도록 허용합니다. 목록의 각 변수는 왼쪽에서 오른쪽 순으로 커서 결과 집합의 해당 열과 연관됩니다. 각 변수의 데이터 형식은 반드시 해당 결과 집합 열의 데이터 형식과 일치하거나 암시적 변환이 지원되어야 합니다. 변수의 개수는 커서 선택 목록의 열 수와 일치해야 합니다.  
  
## <a name="remarks"></a>Remarks  
 `SCROLL` 옵션이 ISO 스타일 `DECLARE CURSOR` 문에서 지정되지 않은 경우 `NEXT`가 유일하게 지원되는 `FETCH` 옵션입니다. `SCROLL`이 ISO 스타일 `DECLARE CURSOR` 문에서 지정되는 경우 모든 `FETCH` 옵션이 지원됩니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] DECLARE 커서 확장을 사용하는 경우에는 다음 규칙이 적용됩니다.  
  
-   `FORWARD_ONLY` 또는 `FAST_FORWARD`를 지정하면 `NEXT`가 유일하게 지원되는 `FETCH` 옵션입니다.  
  
-   `DYNAMIC`, `FORWARD_ONLY` 또는 `FAST_FORWARD`를 지정하지 않고 `KEYSET`, `STATIC` 또는 `SCROLL` 중 하나를 지정하는 경우 모든 `FETCH` 옵션이 지원됩니다.  
  
-   `DYNAMIC SCROLL` 커서는 `ABSOLUTE`를 제외한 모든 `FETCH` 옵션을 지원합니다.  
  
 `@@FETCH_STATUS` 함수는 마지막 `FETCH` 문의 상태를 보고합니다. sp_describe_cursor에 의해 반환되는 커서의 fetch_status 열에도 동일한 정보가 기록됩니다. 해당 데이터에 대해 어떠한 작업을 수행하려고 시도하기 전에 반드시 이 상태 정보를 사용하여 `FETCH` 문에서 반환되는 데이터의 유효성을 확인해야 합니다. 자세한 내용은 [@@FETCH_STATUS&#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)을 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 `FETCH` 권한은 기본적으로 모든 유효한 사용자에게 부여됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-fetch-in-a-simple-cursor"></a>1. 단순 커서에서 FETCH 사용  
 다음 예에서는 `Person.Person` 테이블에 있는 행에 대해 성이 `B`로 시작하는 단순 커서를 선언하고 `FETCH NEXT`를 사용하여 한 행씩 진행하는 방법을 보여 줍니다. `FETCH` 문은 `DECLARE CURSOR`에 지정된 열에 대한 값을 단일 행 결과 집합으로 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch.  
FETCH NEXT FROM contact_cursor;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="b-using-fetch-to-store-values-in-variables"></a>2. FETCH를 사용하여 변수에 값 저장  
 다음 예는 `FETCH` 문의 출력이 클라이언트에게 직접 반환되지 않고 지역 변수에 저장된다는 점 외에는 예 1과 유사합니다. `PRINT` 문은 변수를 한 문자열로 결합하여 클라이언트에 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Declare the variables to store the values returned by FETCH.  
DECLARE @LastName varchar(50), @FirstName varchar(50);  
  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch and store the values in variables.  
-- Note: The variables are in the same order as the columns  
-- in the SELECT statement.   
  
FETCH NEXT FROM contact_cursor  
INTO @LastName, @FirstName;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
  
   -- Concatenate and display the current values in the variables.  
   PRINT 'Contact Name: ' + @FirstName + ' ' +  @LastName  
  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor  
   INTO @LastName, @FirstName;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="c-declaring-a-scroll-cursor-and-using-the-other-fetch-options"></a>3. SCROLL 커서 선언 및 기타 FETCH 옵션 사용  
 다음 예에서는 `SCROLL` 커서를 만들어 `LAST`, `PRIOR`, `RELATIVE` 및 `ABSOLUTE` 옵션 전체에 스크롤 기능을 허용하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Execute the SELECT statement alone to show the   
-- full result set that is used by the cursor.  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
-- Declare the cursor.  
DECLARE contact_cursor SCROLL CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Fetch the last row in the cursor.  
FETCH LAST FROM contact_cursor;  
  
-- Fetch the row immediately prior to the current row in the cursor.  
FETCH PRIOR FROM contact_cursor;  
  
-- Fetch the second row in the cursor.  
FETCH ABSOLUTE 2 FROM contact_cursor;  
  
-- Fetch the row that is three rows after the current row.  
FETCH RELATIVE 3 FROM contact_cursor;  
  
-- Fetch the row that is two rows prior to the current row.  
FETCH RELATIVE -2 FROM contact_cursor;  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [OPEN&#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
