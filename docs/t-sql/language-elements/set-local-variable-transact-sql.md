---
title: SET @local_variable(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SET @local_variable
- variables [SQL Server], assigning
- SET statement, @local_variable
- local variables [SQL Server]
ms.assetid: d410e06e-061b-4c25-9973-b2dc9b60bd85
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 20febb0b33e0da08d8620232195e183c7c5162f3
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65981762"
---
# <a name="set-localvariable-transact-sql"></a>SET @local_variable(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

DECLARE @*local_variable* 문을 사용하여 이전에 만든 지정된 지역 변수를 지정된 값으로 설정합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
SQL Server 및 Azure SQL Database에 대한 구문:

```sql    
SET   
{ @local_variable  
    [ . { property_name | field_name } ] = { expression | udt_name { . | :: } method_name }  
}  
|  
{ @SQLCLR_local_variable.mutator_method  
}  
|  
{ @local_variable  
    {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
}  
|   
  { @cursor_variable =   
    { @cursor_variable | cursor_name   
    | { CURSOR [ FORWARD_ONLY | SCROLL ]   
        [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
        [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
        [ TYPE_WARNING ]   
    FOR select_statement   
        [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]   
      }   
    }  
}   
```  
Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스용 구문:  
```sql  
SET @local_variable {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
```  
  
## <a name="arguments"></a>인수  
**@** _local_variable_  
**cursor**, **text**, **ntext**, **image** 또는 **table**을 제외한 모든 형식의 변수 이름입니다. 변수 이름은 기호( **@** )로 시작해야 합니다. 변수 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 따라야 합니다.  
  
*property_name*  
사용자 정의 형식의 속성입니다.  
  
*field_name*  
사용자 정의 형식의 공용 필드입니다.  
  
*udt_name*  
CLR(공용 언어 런타임) 사용자 정의 형식의 이름입니다.  
  
`{ . | :: }`  
CLR 사용자 정의 형식의 메서드를 지정합니다. 비정적 인스턴스 메서드의 경우 마침표( **.** )를 사용합니다. 정적 메서드의 경우 두 개의 콜론( **::** )을 사용합니다. CLR 사용자 정의 형식의 메서드, 속성 또는 필드를 호출하려면 해당 형식에 대해 EXECUTE 권한이 있어야 합니다.  
  
_method_name_ **(** _argument_ [ **,** ... *n* ] **)**  
하나 이상의 인수를 사용하여 한 형식의 인스턴스 상태를 수정하는 사용자 정의 형식 메서드입니다. 정적 메서드는 공용이어야 합니다.  
  
**@** _SQLCLR_local_variable_  
어셈블리에 형식이 있는 변수입니다. 자세한 내용은 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)를 참조하세요.  
  
*mutator_method*  
개체 상태를 변경할 수 있는 어셈블리의 메서드입니다. SQLMethodAttribute.IsMutator가 이 메서드에 적용됩니다.  
  
`{ += | -= | *= | /= | %= | &= | ^= | |= }`  
복합 할당 연산자:  
  
 +=              더하기 및 할당  
  
 -=              빼기 및 할당  
  
 *=              곱하기 및 할당  
  
 /=              곱하기 및 할당  
  
 %=              나머지 및 할당  
  
 &=              비트 AND 및 할당  
  
 ^=              비트 XOR 및 할당  
  
 |=              비트 OR 및 할당  
  
*expression*  
유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
*cursor_variable*  
커서 변수의 이름입니다. 대상 커서 변수가 이전에 다른 커서를 참조한 경우 이전 참조가 제거됩니다.  
  
*cursor_name*  
DECLARE CURSOR 문을 사용하여 선언한 커서 이름입니다.  
  
CURSOR  
SET 문에 커서 선언이 포함되도록 지정합니다.  
  
SCROLL  
커서가 인출 옵션 FIRST, LAST, NEXT, PRIOR, RELATIVE 및 ABSOLUTE를 모두 지원하도록 지정합니다. FAST_FORWARD도 지정한 경우에는 SCROLL을 지정할 수 없습니다.  
  
FORWARD_ONLY  
커서가 FETCH NEXT 옵션만 지원하도록 지정합니다. 첫 번째 행에서 마지막 행까지 커서를 한 방향으로만 검색합니다. STATIC, KEYSET 또는 DYNAMIC 키워드를 사용하지 않고 FORWARD_ONLY를 지정하면 커서가 DYNAMIC으로 구현됩니다. STATIC, KEYSET 또는 DYNAMIC 키워드가 지정된 경우를 제외하고 FORWARD_ONLY 또는 SCROLL을 지정하지 않으면 FORWARD_ONLY가 기본값입니다. STATIC, KEYSET 및 DYNAMIC 커서의 경우 SCROLL이 기본값입니다.  
  
STATIC  
커서에서 사용할 데이터를 임시로 복사해 주는 커서를 정의합니다. 커서에 대한 모든 요청은 tempdb의 이 임시 테이블에서 응답됩니다. 따라서 기본 테이블에 대한 수정 내용은 해당 커서에 대한 페치에서 반환된 데이터에는 반영되지 않습니다. 또한 이 커서는 수정을 허용하지 않습니다.  
  
KEYSET  
커서가 열릴 때 커서에 있는 행의 멤버 자격과 순서가 고정되도록 지정합니다. 행을 고유하게 식별하는 키 집합이 tempdb의 keysettable 테이블에 작성됩니다. 커서 소유자나 다른 사용자가 기본 테이블에서 키가 아닌 값을 변경하면 그 내용이 커서 소유자가 커서를 스크롤할 때 표시됩니다. 그러나 다른 사용자가 삽입한 데이터는 표시되지 않으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서를 통해 데이터를 삽입할 수 없습니다.  
  
삭제된 행을 가져오려고 하면 -2인 @@FETCH_STATUS를 반환합니다. 커서 외부에서 키 값을 업데이트하는 것은 이전 행을 삭제하고 새 행을 삽입하는 것과 비슷합니다. 새 값이 있는 행이 표시되지 않고 이전 값이 있는 행을 가져오려고 하면 -2인 @@FETCH_STATUS를 반환합니다. WHERE CURRENT OF 절을 지정하여 커서를 통해 업데이트를 수행한 경우에는 새 값이 표시됩니다.  
  
DYNAMIC  
커서 소유자가 커서를 스크롤할 때 결과 집합의 행에 모든 데이터 변경 내용이 반영되도록 커서를 정의합니다. 따라서 인출할 때마다 행의 데이터 값, 순서 및 멤버 자격이 변경될 수 있습니다. 동적 커서에는 절대 페치 및 상대 페치 옵션을 사용할 수 없습니다.  
  
FAST_FORWARD  
최적화를 사용하도록 설정된 FORWARD_ONLY, READ_ONLY 커서를 지정합니다. SCROLL도 지정된 경우에는 FAST_FORWARD를 지정할 수 없습니다.  
  
READ_ONLY  
이 커서를 통해 업데이트할 수 없습니다. UPDATE 또는 DELETE 문의 WHERE CURRENT OF 절에서는 이 커서를 참조할 수 없습니다. 이 옵션은 업데이트할 커서의 기본 기능을 무시합니다.  
  
SCROLL LOCKS  
커서를 통해 현재 위치 업데이트 또는 삭제가 반드시 실행되도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 커서로 읽은 행을 읽을 때 해당 행을 잠가 나중에 수정할 수 있도록 합니다. FAST_FORWARD도 지정된 경우에는 SCROLL_LOCKS를 지정할 수 없습니다.  
  
OPTIMISTIC  
커서로 읽고 있는 행이 업데이트된 경우 커서를 통해 지정된 위치에서 업데이트 또는 삭제가 실패하도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 커서로 행을 읽을 때 행을 잠그지 않습니다. 대신 timestamp 열 값을 비교하거나 테이블에 timestamp 열이 없을 경우 체크섬 값을 비교하여 커서로 읽은 후에 행이 수정되었는지 확인합니다. 행이 수정된 경우 지정된 위치에서 업데이트나 삭제가 실행되지 않습니다. FAST_FORWARD도 지정된 경우에는 OPTIMISTIC을 지정할 수 없습니다.  
  
TYPE_WARNING  
요청한 커서 형식이 다른 형식으로 암시적으로 변환된 경우 클라이언트에게 경고 메시지를 보내도록 지정합니다.  
  
FOR *select_statement*  
커서의 결과 집합을 정의하는 표준 SELECT 문입니다. FOR BROWSE 및 INTO 키워드는 커서 선언의 *select_statement* 내에서 허용되지 않습니다.  
  
DISTINCT, UNION, GROUP BY 또는 HAVING을 사용하거나 *select_list*에 집계 식을 포함하면 커서가 STATIC으로 만들어집니다.  
  
각 기본 테이블에 고유 인덱스가 없고 ISO SCROLL 커서 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] KEYSET 커서가 요청되면 커서가 자동으로 STATIC 커서가 됩니다.  
  
열이 고유 행 식별자가 아닌 ORDER BY 절이 *select_statement* 문에 포함되면, DYNAMIC 커서가 KEYSET 커서로 변환되거나 KEYSET 커서를 열 수 없는 경우 STATIC 커서로 변환됩니다. 이 프로세스는 STATIC 키워드를 사용하지 않고 ISO 구문을 사용해 정의한 커서의 경우에서 수행됩니다.  
  
READ ONLY  
이 커서를 통해 업데이트할 수 없습니다. UPDATE 또는 DELETE 문의 WHERE CURRENT OF 절에서는 이 커서를 참조할 수 없습니다. 이 옵션은 업데이트할 커서의 기본 기능을 무시합니다. 이 키워드는 READ와 ONLY 사이에 밑줄 대신 공백이 있어 앞의 READ_ONLY와는 다른 키워드입니다.  
  
`UPDATE [OF column_name[ ,... n ] ]`  
커서 내에서 업데이트할 수 있는 열을 정의합니다. OF *column_name* [ **,** ...*n*]이 제공되면 나열된 열만 수정할 수 있습니다. 커서가 READ_ONLY로 정의되어 있지 않은 경우 목록을 제공하지 않으면 모든 열을 업데이트할 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
변수를 선언하면 이 변수는 NULL로 초기화됩니다. SET 문을 사용하여 NULL이 아닌 값을 선언된 변수에 할당할 수 있습니다. 변수에 값을 할당한 SET 문은 단일 값을 반환합니다. 여러 변수를 초기화할 때는 지역 변수마다 별도의 SET 문을 사용합니다.  
  
변수는 식에서만 사용할 수 있으며 개체 이름이나 키워드 대신 사용할 수 없습니다. 동적 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 생성하려면 EXECUTE를 실행합니다.  
  
SET **@** _cursor_variable_ 구문 규칙에는 LOCAL 및 GLOBAL 키워드가 없습니다. SET **@** _cursor_variable_ = CURSOR... 구문을 사용하면, 커서가 로컬 커서 데이터베이스 옵션의 기본 설정에 따라 GLOBAL 또는 LOCAL로 만들어집니다.  
  
전역 커서를 참조하는 경우에도 커서 변수는 항상 지역 변수입니다. 커서 변수가 전역 커서를 참조하면 전역 커서 참조 및 로컬 커서 참조를 모두 가지게 됩니다. 자세한 내용은 예 3을 참조하세요.  
  
자세한 내용은 [DECLARE CURSOR&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)를 참조하세요.  
  
할당 연산자의 오른쪽에 변수가 포함된 식이 있고 UPDATE, SELECT 및 RECEIVE 문에 SET이 포함된 곳에는 어디에나 복합 할당 연산자를 사용할 수 있습니다.  
  
값을 연결하려면, 즉 집계 값을 계산하려면 SELECT 문에 변수를 사용하지 마세요. 사용할 경우 예기치 않은 쿼리 결과가 발생할 수 있습니다. SELECT 목록의 모든 식(할당 포함)이 각 출력 행에 대해 정확히 한 번씩 실행되는 것은 아니기 때문입니다. 자세한 내용은 [이 KB 문서](https://support.microsoft.com/kb/287515)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
public 역할의 멤버 자격이 필요합니다. 모든 사용자는 SET **@** _local_variable_을 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-printing-the-value-of-a-variable-initialized-by-using-set"></a>1. SET을 사용하여 초기화된 변수 값 인쇄  
다음 예제에서는 `@myvar` 변수를 만들고, 문자열 값을 변수에 넣고, `@myvar` 변수 값을 출력합니다.  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT @myvar;  
GO  
```  
  
### <a name="b-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>2. SELECT 문에서 SET을 사용하여 값이 할당된 지역 변수 사용  
다음 예에서는 `@state`라는 지역 변수를 만들고 이 변수를 `SELECT` 문에 사용하여 `Oregon` 주에 사는 모든 직원의 이름과 성을 찾습니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @state char(25);  
SET @state = N'Oregon';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name, City  
FROM HumanResources.vEmployee  
WHERE StateProvinceName = @state;  
```  
  
### <a name="c-using-a-compound-assignment-for-a-local-variable"></a>C. 지역 변수에 복합 할당 사용  
다음 두 예는 동일한 결과를 생성합니다. `@NewBalance`라고 하는 지역 변수를 만들고 여기에 10을 곱한 다음 이 지역 변수의 새 값을 `SELECT` 문에 표시합니다. 두 번째 예에서는 복합 할당 연산자를 사용합니다.  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  @NewBalance;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT @NewBalance;  
```  
  
### <a name="d-using-set-with-a-global-cursor"></a>D. 전역 커서와 함께 SET 사용  
다음 예에서는 지역 변수를 만든 후 커서 변수를 전역 커서 이름으로 설정합니다.  
  
```  
DECLARE my_cursor CURSOR GLOBAL   
FOR SELECT * FROM Purchasing.ShipMethod  
DECLARE @my_variable CURSOR ;  
SET @my_variable = my_cursor ;   
--There is a GLOBAL cursor declared(my_cursor) and a LOCAL variable  
--(@my_variable) set to the my_cursor cursor.  
DEALLOCATE my_cursor;   
--There is now only a LOCAL variable reference  
--(@my_variable) to the my_cursor cursor.  
```  
  
### <a name="e-defining-a-cursor-by-using-set"></a>E. SET을 사용하여 커서 정의  
다음 예에서는 `SET` 문을 사용하여 커서를 정의합니다.  
  
```  
DECLARE @CursorVar CURSOR;  
  
SET @CursorVar = CURSOR SCROLL DYNAMIC  
FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN @CursorVar;  
  
FETCH NEXT FROM @CursorVar;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM @CursorVar  
END;  
  
CLOSE @CursorVar;  
DEALLOCATE @CursorVar;  
```  
  
### <a name="f-assigning-a-value-from-a-query"></a>F. 쿼리에서 값 할당  
다음 예에서는 쿼리를 사용하여 변수에 값을 할당합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM Sales.Customer);  
SELECT @rows;  
```  
  
### <a name="g-assigning-a-value-to-a-user-defined-type-variable-by-modifying-a-property-of-the-type"></a>G. 사용자 정의 형식의 속성을 수정하여 사용자 정의 형식 변수에 값 할당  
다음 예에서는 사용자 정의 형식의 `Point` 속성 값을 수정하여 사용자 정의 형식 `X`의 값을 설정합니다.  
  
```  
DECLARE @p Point;  
SET @p.X = @p.X + 1.1;  
SELECT @p;  
GO  
```  
  
### <a name="h-assigning-a-value-to-a-user-defined-type-variable-by-invoking-a-method-of-the-type"></a>H. 사용자 정의 형식의 메서드를 호출하여 사용자 정의 형식 변수에 값 할당  
다음 예제에서는 형식의 `SetXY` 메서드를 호출하여 **point** 사용자 정의 형식의 값을 설정합니다.  
  
```  
DECLARE @p Point;  
SET @p=point.SetXY(23.5, 23.5);  
```  
  
### <a name="i-creating-a-variable-for-a-clr-type-and-calling-a-mutator-method"></a>9. CLR 유형에 대한 변수를 만들고 변경자(mutator) 메서드 호출  
다음 예에서는 유형 `Point`에 대한 변수를 만들고 `Point`에서 변경자(mutator) 메서드를 실행합니다.  
  
```  
CREATE ASSEMBLY mytest from 'c:\test.dll' WITH PERMISSION_SET = SAFE  
CREATE TYPE Point EXTERNAL NAME mytest.Point  
GO  
DECLARE @p Point = CONVERT(Point, '')  
SET @p.SetXY(22, 23);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-printing-the-value-of-a-variable-initialized-by-using-set"></a>J. SET을 사용하여 초기화된 변수 값 인쇄  
다음 예제에서는 `@myvar` 변수를 만들고, 문자열 값을 변수에 넣고, `@myvar` 변수 값을 출력합니다.  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT top 1 @myvar FROM sys.databases;  
  
```  
  
### <a name="k-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>11. SELECT 문에서 SET을 사용하여 값이 할당된 지역 변수 사용  
다음 예제에서는 `@dept`라는 지역 변수를 만들고, 이 지역 변수를 `SELECT` 문에 사용하여 `Marketing` 부서에서 근무하는 모든 직원의 이름과 성을 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @dept char(25);  
SET @dept = N'Marketing';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name  
FROM DimEmployee   
WHERE DepartmentName = @dept;  
```  
  
### <a name="l-using-a-compound-assignment-for-a-local-variable"></a>12. 지역 변수에 복합 할당 사용  
다음 두 예는 동일한 결과를 생성합니다. `@NewBalance`라고 하는 지역 변수를 만들고 여기에 `10`을 곱한 다음 이 지역 변수의 새 값을 `SELECT` 문으로 표시합니다. 두 번째 예에서는 복합 할당 연산자를 사용합니다.  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  TOP 1 @NewBalance FROM sys.tables;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT TOP 1 @NewBalance FROM sys.tables;  
```  
  
### <a name="m-assigning-a-value-from-a-query"></a>13. 쿼리에서 값 할당  
다음 예에서는 쿼리를 사용하여 변수에 값을 할당합니다.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM dbo.DimCustomer);  
SELECT TOP 1 @rows FROM sys.tables;  
```  
  
## <a name="see-also"></a>참고 항목  
[복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
[EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
[SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
[SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

