---
title: OUTPUT 절(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OUTPUT_TSQL
- OUTPUT
dev_langs:
- TSQL
helpviewer_keywords:
- displaying updated rows
- INSERT statement [SQL Server], OUTPUT clause
- outputs [SQL Server]
- OUTPUT clause
- row additions [SQL Server], OUTPUT clause
- viewing updated rows
- row deletions [SQL Server], OUTPUT clause
- viewing deleted rows
- DELETE statement [SQL Server], OUTPUT clause
- row updates [SQL Server]
- displaying inserted rows
- viewing inserted rows
- displaying deleted rows
- UPDATE statement [SQL Server], OUTPUT clause
ms.assetid: 41b9962c-0c71-4227-80a0-08fdc19f5fe4
caps.latest.revision: 94
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 87906714cbca4fc62a1593e19772d8c9c8a8354c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="output-clause-transact-sql"></a>OUTPUT 절(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  INSERT, UPDATE, DELETE 또는 MERGE 문의 영향을 받는 각 행의 정보 또는 각 행을 기반으로 하는 식을 반환합니다. 이러한 결과를 처리 응용 프로그램에 반환하여 확인 메시지, 보관 및 기타 응용 프로그램 요구 사항을 충족시키는 데 사용할 수 있습니다. 결과를 테이블 또는 테이블 변수에 삽입할 수도 있습니다. 또한 중첩된 INSERT, UPDATE, DELETE 또는 MERGE 문에서 OUTPUT 절의 결과를 캡처하고 그 결과를 대상 테이블이나 뷰에 삽입할 수 있습니다.  
  
> [!NOTE]  
>  OUTPUT 절이 있는 UPDATE, INSERT 또는 DELETE 문은 문에 오류가 발생하여 롤백되어도 클라이언트에 행을 반환합니다. 문을 실행할 때 오류가 발생하는 경우에는 해당 결과를 사용하면 안 됩니다.  
  
 **사용 대상:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
<OUTPUT_CLAUSE> ::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table } [ ( column_list ) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
<dml_select_list> ::=  
{ <column_name> | scalar_expression } [ [AS] column_alias_identifier ]  
    [ ,...n ]  
  
<column_name> ::=  
{ DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>인수  
 @*table_variable*  
 반환된 행이 호출자에게 반환되는 대신 삽입되는 **table** 변수를 지정합니다. @*table_variable*은 INSERT, UPDATE, DELETE 또는 MERGE 문 앞에 선언해야 합니다.  
  
 *column_list*가 지정되지 않으면 **table** 변수에 OUTPUT 결과 집합과 동일한 수의 열이 있어야 합니다. 단, ID 및 계산 열은 건너뛰므로 예외입니다. *column_list*가 지정되면 생략된 모든 열에 Null 값을 허용하거나 기본값을 할당해야 합니다.  
  
 **table** 변수에 대한 자세한 내용은 [table&#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)을 참조하세요.  
  
 *output_table*  
 반환된 행을 호출자에 반환하는 대신 삽입할 테이블을 지정합니다. *output_table*은 임시 테이블일 수 있습니다.  
  
 *output_table*가 지정되지 않으면 테이블에 OUTPUT 결과 집합과 동일한 수의 열이 있어야 합니다. 단, ID 및 계산 열은 예외이며 이 열은 건너뛰어야 합니다. *column_list*가 지정되면 생략된 모든 열에 Null 값을 허용하거나 기본값을 할당해야 합니다.  
  
 *output_table*은 다음 작업을 수행할 수 없습니다.  
  
-   활성화된 트리거를 정의할 수 없습니다.  
  
-   FOREIGN KEY 제약 조건의 어느 쪽에도 참여할 수 없습니다.  
  
-   CHECK 제약 조건 또는 활성화된 규칙을 가질 수 없습니다.  
  
*column_list*  
 INTO 절에 지정되는 대상 테이블의 열 이름 목록입니다(옵션). [INSERT](../../t-sql/statements/insert-transact-sql.md) 문에서 허용되는 열 목록과 비슷합니다.  
  
 *scalar_expression*  
 단일 값으로 계산되는 기호 및 연산자의 조합입니다. 집계 함수는 *scalar_expression*에 허용되지 않습니다.  
  
 수정되는 테이블의 열에 대한 모든 참조는 INSERTED 또는 DELETED 접두사를 사용해 정규화되어야 합니다.  
  
 *column_alias_identifier*  
 열 이름을 참조하기 위해 사용되는 대체 이름입니다.  
  
 DELETED  
 업데이트 또는 삭제 연산에 의해 삭제된 값을 지정하는 열 접두사입니다. DELETED가 접두사로 사용된 열은 UPDATE, DELETE 또는 MERGE 문이 완료되기 이전의 값을 반영합니다.  
  
 DELETED는 INSERT 문에서 OUTPUT 절과 함께 사용할 수 없습니다.  
  
 INSERTED  
 삽입 또는 업데이트 연산에 의해 추가된 값을 지정하는 열 접두사입니다. INSERTED가 접두사로 사용된 열은 UPDATE, INSERT 또는 MERGE 문이 완료되었으나 트리거가 실행되기 이전의 값을 반영합니다.  
  
 INSERTED는 DELETE 문에서 OUTPUT 절과 함께 사용할 수 없습니다.  
  
 *from_table_name*  
 업데이트 또는 삭제할 행을 지정하는 데 사용되는 DELETE, UPDATE 또는 MERGE 문의 FROM 절에 포함된 테이블을 지정하는 열 접두사입니다.  
  
 변경되는 테이블을 FROM 절에도 지정할 경우 해당 테이블의 열에 대한 모든 참조는 INSERTED 또는 DELETED 접두사를 사용해 정규화해야 합니다.  
  
 \*  
 삭제, 삽입 또는 업데이트 동작의 영향을 받은 모든 열이 테이블에 존재하는 순서대로 반환되도록 지정합니다.  
  
 예를 들어 다음 DELETE 문에서 `OUTPUT DELETED.*`는 `ShoppingCartItem` 테이블에서 삭제된 모든 열을 반환합니다.  
  
```  
DELETE Sales.ShoppingCartItem  
    OUTPUT DELETED.*;  
```  
  
 *column_name*  
 명시적 열 참조입니다. 수정되는 테이블에 대한 모든 참조는 INSERTED 또는 DELETED 접두사로 적절히 한정되어야 합니다(예: INSERTED**.***column_name*).  
  
 $action  
 MERGE 문에만 사용할 수 있습니다. 해당 행에서 수행된 작업에 따라 각 행에 대해 'INSERT', 'UPDATE' 또는 'DELETE' 값 중 하나를 반환하는 MERGE 문의 OUTPUT 절에 **nvarchar(10)** 형식의 열을 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 OUTPUT \<dml_select_list> 절 및 OUTPUT \<dml_select_list> INTO { **@***table_variable* | *output_table* } 절은 단일 INSERT, UPDATE, DELETE 또는 MERGE 문에서 정의할 수 있습니다.  
  
> [!NOTE]  
>  다르게 지정되지 않는 이상 OUTPUT 절에 대한 참조는 OUTPUT 절 및 OUTPUT INTO 절 모두를 참조합니다.  
  
 OUTPUT 절은 INSERT 또는 UPDATE 작업 후에 ID 또는 계산 열의 값을 가져오는 데 유용합니다.  
  
 계산 열이 \<dml_select_list>에 포함되면 출력 테이블 또는 테이블 변수의 해당 열은 계산 열이 아닙니다. 새 열의 값은 문이 실행된 시점에 계산된 값입니다.  
  
 변경 사항이 테이블에 적용되는 순서 및 행이 출력 테이블 또는 테이블 변수에 삽입되는 순서가 일치할 것이라는 보장은 없습니다.  
  
 매개 변수 또는 변수가 UPDATE 문의 일부로 수정되면 OUTPUT 절은 항상 수정된 값 대신 문이 실행되기 전의 매개 변수 또는 변수의 값을 반환합니다.  
  
 OUTPUT은 WHERE CURRENT OF 구문을 사용하는 커서에 위치한 UPDATE 또는 DELETE 문과 함께 사용할 수 있습니다.  
  
 OUTPUT 절을 지원하지 않는 문은 다음과 같습니다.  
  
-   분할된 로컬 뷰, 배포된 분할된 뷰 또는 원격 테이블을 참조하는 DML 문  
  
-   EXECUTE 문이 포함된 INSERT 문  
  
-   데이터베이스 호환성 수준이 100으로 설정된 경우에는 OUTPUT 절에 전체 텍스트 조건자가 허용되지 않습니다.  
  
-   OUTPUT INTO 절은 뷰 또는 행 집합 함수로의 삽입에 사용할 수 없습니다.  
  
-   테이블을 대상으로 가진 OUTPUT INTO 절이 있는 사용자 정의 함수는 만들 수 없습니다.  
  
 비결정적 동작을 방지하기 위해 OUTPUT 절은 다음과 같은 참조를 포함할 수 없습니다.  
  
-   사용자 또는 시스템 데이터 액세스를 수행하거나 이러한 액세스를 수행하는 것으로 간주되는 하위 쿼리 또는 사용자 정의 함수입니다. 스키마 바운드가 아닌 사용자 정의 함수는 데이터 액세스를 수행하는 것으로 간주됩니다.  
  
-   해당 열이 다음 중 한 가지 방법으로 정의된 경우 뷰 또는 인라인 테이블 반환 함수의 열입니다.  
  
    -   하위 쿼리  
  
    -   사용자 또는 시스템 데이터 액세스를 수행하거나 이러한 액세스를 수행하는 것으로 간주되는 사용자 정의 함수  
  
    -   해당 정의에서 사용자 또는 시스템 데이터 액세스를 수행하는 사용자 정의 함수가 포함된 계산 열  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 OUTPUT 절에서 이러한 열을 감지하면 4186 오류가 발생합니다.   
  
## <a name="inserting-data-returned-from-an-output-clause-into-a-table"></a>OUTPUT 절에서 반환된 데이터를 테이블에 삽입  
 중첩된 INSERT, UPDATE, DELETE 또는 MERGE 문에서 OUTPUT 절의 결과를 캡처하고 그 결과를 대상 테이블에 삽입하는 경우 다음 사항을 고려하세요.  
  
-   전체 작업은 원자성을 갖습니다. INSERT 문과 OUTPUT 절을 포함하는 중첩된 DML 문 중 하나라도 실행되지 않으면 전체 문이 실패합니다.  
  
-   다음과 같은 제한 사항이 외부 INSERT 문의 대상에 적용됩니다.  
  
    -   대상은 원격 테이블, 뷰 또는 공통 테이블 식일 수 없습니다.  
  
    -   대상은 FOREIGN KEY 제약 조건을 갖거나 FOREIGN KEY 제약 조건에 의해 참조될 수 없습니다.  
  
    -   대상에 대해서는 트리거를 정의할 수 없습니다.  
  
    -   대상은 트랜잭션 복제에 대한 병합 복제 또는 업데이트할 수 있는 구독에 참여할 수 없습니다.  
  
-   다음과 같은 제한 사항이 중첩된 DML 문에 적용됩니다.  
  
    -   대상은 원격 테이블 또는 분할된 뷰일 수 없습니다.  
  
    -   원본 자체에는 \<dml_table_source> 절이 포함될 수 없습니다.  
  
-   OUTPUT INTO 절은 \<dml_table_source> 절이 포함된 INSERT 문에서 지원되지 않습니다.  
  
-   @@ROWCOUNT는 외부 INSERT 문에서만 삽입된 행을 반환합니다.  
  
-   @@IDENTITY, SCOPE_IDENTITY 및 IDENT_CURRENT는 중첩된 DML 문에서만 생성된 ID 값만 반환하고, 외부 INSERT 문에서 생성된 ID 값은 반환하지 않습니다.  
  
-   외부 INSERT 문 자체에서 크게 변경된 경우에도 쿼리 알림은 문을 단일 엔터티로 취급하며 작성되는 메시지의 유형은 중첩된 DML의 유형이 됩니다.  
  
-   \<dml_table_source> 절에서 SELECT 및 WHERE 절에는 하위 쿼리, 집계 함수, 순위 함수, 전체 텍스트 조건자, 데이터 액세스를 수행하는 사용자 정의 함수 또는 TEXTPTR 함수가 포함될 수 없습니다.  

## <a name="parallelism"></a>Parallelism
 결과를 클라이언트에 반환하는 OUTPUT 절은 항상 직렬 계획을 사용합니다.

호환성 수준 130 이상으로 설정된 데이터베이스의 컨텍스트에서 INSERT...SELECT 작업이 SELECT 문에 WITH (TABLOCK) 힌트를 사용하고 OUTPUT…INTO를 사용하여 임시 또는 사용자 테이블에 삽입하는 경우, INSERT…SELECT에 대한 목표 테이블은 하위 트리 비용에 따라 병렬 처리에 적합합니다.  OUTPUT INTO 절에서 참조되는 목표 테이블은 병렬 처리에 적합하지 않습니다. 
 
## <a name="triggers"></a>트리거  
 OUTPUT에서 반환된 열에는 INSERT, UPDATE 또는 DELETE 문이 완료된 후, 그리고 트리거가 실행되기 전의 데이터가 반영됩니다.  
  
 INSTEAD OF 트리거의 경우 트리거 작업의 결과로 아무런 수정 사항이 없음에도 불구하고 INSERT, UPDATE 또는 DELETE가 실제로 발생한 것처럼 반환 결과가 생성됩니다. OUTPUT 절이 포함된 문이 트리거 본문에 사용되면 OUTPUT과 연결된 INSERTED 및 DELETED 테이블과의 열 참조 중복을 피하기 위해 트리거가 삽입 및 삭제한 테이블을 참조하는 데 테이블 별칭이 사용됩니다.  
  
 INTO 키워드를 지정하지 않은 채 OUTPUT 절을 지정하면 DML 작업의 대상이 지정된 DML 동작을 위해 정의된 활성화된 트리거를 가질 수 없습니다. 예를 들어 UPDATE 문에 OUTPUT 절이 정의되면 대상 테이블은 어떤 활성화된 UPDATE 트리거도 가질 수 없습니다.  
  
 sp_configure 옵션인 트리거에서 결과 반환 허용 안 함이 설정되어 있으면 INTO 절이 없는 OUTPUT 절이 트리거 내부에서 호출되었을 때 문이 실패합니다.  
  
## <a name="data-types"></a>데이터 형식  
 OUTPUT 절은 큰 개체 데이터 형식, 즉 **nvarchar(max)**, **varchar(max)**, **varbinary(max)**, **text**, **ntext**, **image** 및 **xml**을 지원합니다. UPDATE 문에서 .WRITE 절을 사용하여 **nvarchar(max)**, **varchar(max)** 또는 **varbinary(max)** 열을 수정하는 경우, 값의 이전 및 이후 이미지 전체가 참조되면 해당 이미지가 반환됩니다. TEXTPTR( ) 함수는 OUTPUT 절의 **text**, **ntext**또는 **image** 열에 대한 식의 일부로 나타날 수 없습니다.  
  
## <a name="queues"></a>큐  
 테이블을 큐 또는 중간 결과 집합의 저장을 위해 사용하는 응용 프로그램에서 OUTPUT을 사용할 수 있습니다. 이 경우 응용 프로그램은 지속적으로 테이블에 행을 추가하거나 제거합니다. 다음 예에서는 삭제된 행을 호출하는 응용 프로그램에 반환하기 위해 DELETE 문에 OUTPUT 절을 사용합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DELETE TOP(1) dbo.DatabaseLog WITH (READPAST)  
OUTPUT deleted.*  
WHERE DatabaseLogID = 7;  
GO  
  
```  
  
 이 예에서는 큐로 사용되는 테이블에서 행을 삭제하고 삭제된 값을 처리하는 응용 프로그램에 반환하는 과정을 한 번의 작동으로 수행합니다. 이 밖에도 스택 구현을 위해 테이블을 사용하는 등 다른 응용도 가능합니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 DML 문이 OUTPUT 절을 사용해 처리 및 반환하는 행의 순서 유지를 보장하지 않습니다. 원하는 용도에 맞게 적절한 WHERE 절을 포함하거나 DML 작업에 여러 행을 사용하기 위해 적절히 정규화할 책임은 응용 프로그램의 몫입니다. 다음 예에서는 하위 쿼리를 사용하며 필요한 정렬 구현을 위해 각 `DatabaseLogID` 열이 고유한 특성을 가짐을 가정합니다.  
  
```  
USE tempdb;  
GO  
CREATE TABLE dbo.table1  
(  
    id INT,  
    employee VARCHAR(32)  
);  
GO  
  
INSERT INTO dbo.table1 VALUES   
      (1, 'Fred')  
     ,(2, 'Tom')  
     ,(3, 'Sally')  
     ,(4, 'Alice');  
GO  
  
DECLARE @MyTableVar TABLE  
(  
    id INT,  
    employee VARCHAR(32)  
);  
  
PRINT 'table1, before delete'   
SELECT * FROM dbo.table1;  
  
DELETE FROM dbo.table1  
OUTPUT DELETED.* INTO @MyTableVar  
WHERE id = 4 OR id = 2;  
  
PRINT 'table1, after delete'  
SELECT * FROM dbo.table1;  
  
PRINT '@MyTableVar, after delete'  
SELECT * FROM @MyTableVar;  
  
DROP TABLE dbo.table1;  
  
--Results  
--table1, before delete  
--id          employee  
------------- ------------------------------  
--1           Fred  
--2           Tom  
--3           Sally  
--4           Alice  
--  
--table1, after delete  
--id          employee  
------------- ------------------------------  
--1           Fred  
--3           Sally  
--@MyTableVar, after delete  
--id          employee  
------------- ------------------------------  
--2           Tom  
--4           Alice  
  
```  
  
> [!NOTE]  
>  여러 개의 응용 프로그램에서 한 테이블에 대해 파괴 읽기를 허용하는 경우 UPDATE 및 DELETE 문에서 READPAST 테이블 힌트를 사용하세요. 이렇게 하면 다른 응용 프로그램이 이미 테이블의 첫 번째 정규화 레코드를 읽고 있는 경우 발생할 수 있는 잠금 문제를 방지합니다.  
  
## <a name="permissions"></a>사용 권한  
 SELECT 권한은 \<dml_select_list>를 통해 검색되거나 \<scalar_expression>에서 사용되는 모든 열에 필요합니다.  
  
 INSERT 권한은 \<output_table>에 지정된 모든 테이블에 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-output-into-with-a-simple-insert-statement"></a>1. 간단한 INSERT 문과 함께 OUTPUT INTO 사용  
 다음 예제에서는 `ScrapReason` 테이블에 행을 삽입하고, `OUTPUT` 절을 사용하여 명령문의 결과를 `@MyTableVar``table` 변수에 반환합니다. `ScrapReasonID` 열은 IDENTITY 속성을 사용해 정의되기 때문에 이 열의 값은 `INSERT` 문에서 지정되지 않습니다. 하지만 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 의해 생성된 해당 열의 값은 `OUTPUT` 열의 `inserted.ScrapReasonID` 절에서 반환됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table( NewScrapReasonID smallint,  
                           Name varchar(50),  
                           ModifiedDate datetime);  
INSERT Production.ScrapReason  
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate  
        INTO @MyTableVar  
VALUES (N'Operator error', GETDATE());  
  
--Display the result set of the table variable.  
SELECT NewScrapReasonID, Name, ModifiedDate FROM @MyTableVar;  
--Display the result set of the table.  
SELECT ScrapReasonID, Name, ModifiedDate   
FROM Production.ScrapReason;  
GO  
  
```  
  
### <a name="b-using-output-with-a-delete-statement"></a>2. DELETE 문과 함께 OUTPUT 사용  
 다음 예에서는 `ShoppingCartItem` 테이블의 모든 행을 삭제합니다. `OUTPUT deleted.*` 절은 `DELETE` 문의 결과로 삭제된 행의 모든 열을 호출하는 응용 프로그램에 반환하도록 지정합니다. 이어지는 `SELECT` 문은 `ShoppingCartItem` 테이블의 삭제 작업 결과를 확인합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DELETE Sales.ShoppingCartItem  
OUTPUT DELETED.*   
WHERE ShoppingCartID = 20621;  
  
--Verify the rows in the table matching the WHERE clause have been deleted.  
SELECT COUNT(*) AS [Rows in Table] FROM Sales.ShoppingCartItem WHERE ShoppingCartID = 20621;  
GO  
  
```  
  
### <a name="c-using-output-into-with-an-update-statement"></a>3. UPDATE 문과 함께 OUTPUT INTO 사용  
 다음 예에서는 `VacationHours` 테이블에 있는 처음 10개 행의 `Employee` 열을 25% 업데이트합니다. `OUTPUT` 절은 `deleted.VacationHours` 열에서 `UPDATE` 문을 적용하기 전에 있었던 `VacationHours` 값과 `inserted.VacationHours` 열에서 업데이트된 값을 `@MyTableVar``table` 변수에 반환합니다.  
  
 각각 `SELECT`의 값과 `@MyTableVar` 테이블의 업데이트 작업 결과를 반환하는 두 개의 `Employee` 문이 이어집니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()   
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
  
```  
  
### <a name="d-using-output-into-to-return-an-expression"></a>4. OUTPUT INTO를 사용하여 식 반환  
 예 3을 기반으로 만들어진 다음 예에서는 업데이트된 `OUTPUT` 값과 업데이트가 적용되기 이전의 `VacationHours` 값 간의 차이를 나타내는 식을 `VacationHours` 절에 정의합니다. 이 식의 값은 `@MyTableVar``table` 열의 `VacationHoursDifference` 변수에 반환됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    VacationHoursDifference int,  
    ModifiedDate datetime);  
  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()  
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.VacationHours - deleted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours,   
    VacationHoursDifference, ModifiedDate  
FROM @MyTableVar;  
GO  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
  
```  
  
### <a name="e-using-output-into-with-fromtablename-in-an-update-statement"></a>5. UPDATE 문에 from_table_name과 함께 OUTPUT INTO 사용  
 다음 예제에서는 지정된 `ProductID` 및 `ScrapReasonID`가 있는 모든 작업 순서에 대해 `WorkOrder` 테이블의 `ScrapReasonID` 열을 업데이트합니다. `OUTPUT INTO` 절은 업데이트되는 테이블인 `WorkOrder`의 값과 더불어 `Product` 테이블의 값을 반환합니다. 업데이트할 행을 지정하기 위해 `Product` 테이블이 `FROM` 절에 사용됩니다. `WorkOrder` 테이블에는 `AFTER UPDATE` 트리거가 정의되어 있으므로 `INTO` 키워드가 필요합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTestVar table (  
    OldScrapReasonID int NOT NULL,   
    NewScrapReasonID int NOT NULL,   
    WorkOrderID int NOT NULL,  
    ProductID int NOT NULL,  
    ProductName nvarchar(50)NOT NULL);  
  
UPDATE Production.WorkOrder  
SET ScrapReasonID = 4  
OUTPUT deleted.ScrapReasonID,  
       inserted.ScrapReasonID,   
       inserted.WorkOrderID,  
       inserted.ProductID,  
       p.Name  
    INTO @MyTestVar  
FROM Production.WorkOrder AS wo  
    INNER JOIN Production.Product AS p   
    ON wo.ProductID = p.ProductID   
    AND wo.ScrapReasonID= 16  
    AND p.ProductID = 733;  
  
SELECT OldScrapReasonID, NewScrapReasonID, WorkOrderID,   
    ProductID, ProductName   
FROM @MyTestVar;  
GO  
  
```  
  
### <a name="f-using-output-into-with-fromtablename-in-a-delete-statement"></a>6. DELETE 문에 from_table_name과 함께 OUTPUT INTO 사용  
 다음 예에서는 `ProductProductPhoto` 문의 `FROM` 절에 정의된 검색 조건에 따라 `DELETE` 테이블의 행을 삭제합니다. `OUTPUT` 절은 삭제되는 테이블인 `deleted.ProductID` 및 `deleted.ProductPhotoID`의 열과 더불어 `Product` 테이블의 열을 반환합니다. 이 테이블은 `FROM` 절에서 삭제할 행을 지정하기 위해 사용됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
    WHERE p.ProductModelID BETWEEN 120 and 130;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, ProductModelID, PhotoID   
FROM @MyTableVar  
ORDER BY ProductModelID;  
GO  
  
```  
  
### <a name="g-using-output-into-with-a-large-object-data-type"></a>7. 큰 개체 데이터 형식과 함께 OUTPUT INTO 사용  
 다음 예에서는 `DocumentSummary` 절을 사용해 `nvarchar(max)` 테이블의 `Production.Document` 열인 `.WRITE`의 부분 값을 업데이트합니다. 대체 단어, 기존 데이터에서 대체할 단어의 시작 위치(오프셋), 그리고 대체할 문자 수(길이)를 지정함으로써 `components`가 `features`로 대체됩니다. 이 예제에서는 `OUTPUT` 절을 사용해 `DocumentSummary` 열의 이전 및 이후 이미지를 `@MyTableVar``table` 변수에 반환합니다. `DocumentSummary` 열의 이전 및 이후 이미지 전체가 반환됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    SummaryBefore nvarchar(max),  
    SummaryAfter nvarchar(max));  
  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
OUTPUT deleted.DocumentSummary,   
       inserted.DocumentSummary   
    INTO @MyTableVar  
WHERE Title = N'Front Reflector Bracket Installation';  
  
SELECT SummaryBefore, SummaryAfter   
FROM @MyTableVar;  
GO  
  
```  
  
### <a name="h-using-output-in-an-instead-of-trigger"></a>8. INSTEAD OF 트리거에서 OUTPUT 사용  
 다음 예에서는 트리거에 `OUTPUT` 절을 사용하여 트리거 작업 결과를 반환합니다. 먼저 `ScrapReason` 테이블에서 뷰를 만들고 해당 뷰에서 사용자가 기본 테이블의 `INSTEAD OF INSERT` 열만 수정할 수 있게 하는 `Name` 트리거를 정의합니다. `ScrapReasonID` 열은 기본 테이블의 `IDENTITY` 열이기 때문에 트리거는 사용자가 제공한 값을 무시합니다. 대신 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 자동으로 올바른 값을 생성합니다. 또한 사용자가 제공한 `ModifiedDate` 값 역시 무시되고 현재 날짜로 설정됩니다. `OUTPUT` 절은 `ScrapReason` 테이블에 실제로 삽입된 값을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('dbo.vw_ScrapReason','V') IS NOT NULL  
    DROP VIEW dbo.vw_ScrapReason;  
GO  
CREATE VIEW dbo.vw_ScrapReason  
AS (SELECT ScrapReasonID, Name, ModifiedDate  
    FROM Production.ScrapReason);  
GO  
CREATE TRIGGER dbo.io_ScrapReason   
    ON dbo.vw_ScrapReason  
INSTEAD OF INSERT  
AS  
BEGIN  
--ScrapReasonID is not specified in the list of columns to be inserted   
--because it is an IDENTITY column.  
    INSERT INTO Production.ScrapReason (Name, ModifiedDate)  
        OUTPUT INSERTED.ScrapReasonID, INSERTED.Name,   
               INSERTED.ModifiedDate  
    SELECT Name, getdate()  
    FROM inserted;  
END  
GO  
INSERT vw_ScrapReason (ScrapReasonID, Name, ModifiedDate)  
VALUES (99, N'My scrap reason','20030404');  
GO  
  
```  
  
 다음은 2004년 4월 12일('`2004-04-12'`)에 생성된 결과 집합입니다. `ScrapReasonIDActual` 및 `ModifiedDate` 열은 `INSERT` 문에서 제공된 값 대신 트리거 작업에 의해 생성된 값을 반영합니다.  
  
 ```
 ScrapReasonID  Name             ModifiedDate  
 -------------  ---------------- -----------------------  
 17             My scrap reason  2004-04-12 16:23:33.050
 ```  
  
### <a name="i-using-output-into-with-identity-and-computed-columns"></a>9. ID 및 계산 열과 함께 OUTPUT INTO 사용  
 다음 예에서는 `EmployeeSales` 테이블을 만들고 `INSERT` 문에 `SELECT` 문을 사용하여 이 테이블에 여러 개의 행을 삽입한 후 원본 테이블에서 데이터를 검색합니다. `EmployeeSales` 테이블에는 ID 열(`EmployeeID`)과 계산 열(`ProjectedSales`)이 포함되어 있습니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   int IDENTITY (1,5)NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales AS CurrentSales * 1.10   
);  
GO  
DECLARE @MyTableVar table(  
  EmployeeID   int NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales money NOT NULL  
  );  
  
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)  
  OUTPUT INSERTED.LastName,   
         INSERTED.FirstName,   
         INSERTED.CurrentSales  
  INTO @MyTableVar  
    SELECT c.LastName, c.FirstName, sp.SalesYTD  
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY c.LastName, c.FirstName;  
  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM @MyTableVar;  
GO  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM dbo.EmployeeSales;  
GO  
  
```  
  
### <a name="j-using-output-and-output-into-in-a-single-statement"></a>10. 단일 문에서 OUTPUT 및 OUTPUT INTO 사용  
 다음 예에서는 `ProductProductPhoto` 문의 `FROM` 절에 정의된 검색 조건에 따라 `DELETE` 테이블의 행을 삭제합니다. `OUTPUT INTO` 절은 삭제되는 테이블(`deleted.ProductID` 및 `deleted.ProductPhotoID`)의 열과 `Product` 테이블의 열을 `@MyTableVar``table` 변수에 반환합니다. `Product` 테이블은 `FROM` 절에서 삭제할 행을 지정하기 위해 사용됩니다. `OUTPUT` 절은 `deleted.ProductID` 및 `deleted.ProductPhotoID` 열, 그리고 `ProductProductPhoto` 테이블에서 행을 삭제한 날짜 및 시간을 호출하는 응용 프로그램에 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
OUTPUT DELETED.ProductID, DELETED.ProductPhotoID, GETDATE() AS DeletedDate   
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
WHERE p.ProductID BETWEEN 800 and 810;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, PhotoID, ProductModelID   
FROM @MyTableVar;  
GO  
  
```  
  
### <a name="k-inserting-data-returned-from-an-output-clause"></a>11. OUTPUT 절에서 반환된 데이터 삽입  
 다음 예에서는 `OUTPUT` 문의 `MERGE` 절에서 반환되는 데이터를 캡처하고 이 데이터를 다른 테이블에 삽입합니다. `MERGE` 문은 `Quantity` 테이블에서 처리하는 순서대로 `ProductInventory` 테이블의 `SalesOrderDetail` 열을 매일 업데이트합니다. 또한 재고가 `0` 이하로 떨어지는 제품의 행을 삭제합니다. 이 예에서는 삭제된 행을 캡처한 후 다른 `ZeroInventory` 테이블에 삽입하여 재고가 없는 제품을 추적합니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Production.ZeroInventory', N'U') IS NOT NULL  
    DROP TABLE Production.ZeroInventory;  
GO  
--Create ZeroInventory table.  
CREATE TABLE Production.ZeroInventory (DeletedProductID int, RemovedOnDate DateTime);  
GO  
  
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)  
SELECT ProductID, GETDATE()  
FROM  
(   MERGE Production.ProductInventory AS pi  
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
           JOIN Sales.SalesOrderHeader AS soh  
           ON sod.SalesOrderID = soh.SalesOrderID  
           AND soh.OrderDate = '20070401'  
           GROUP BY ProductID) AS src (ProductID, OrderQty)  
    ON (pi.ProductID = src.ProductID)  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0  
        THEN DELETE  
    WHEN MATCHED  
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)  
WHERE Action = 'DELETE';  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were inserted';  
GO  
SELECT DeletedProductID, RemovedOnDate FROM Production.ZeroInventory;  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
