---
title: COLUMNS_UPDATED(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLUMNS_UPDATED_TSQL
- COLUMNS_UPDATED
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS_UPDATED function
- testing columns
- column testing [SQL Server]
- updated columns
ms.assetid: 765fde44-1f95-4015-80a4-45388f18a42c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 02cc6ae014dc52df01e08c13b9610be5ffa50c6b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720321"
---
# <a name="columnsupdated-transact-sql"></a>COLUMNS_UPDATED(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 테이블이나 뷰에서 삽입되거나 업데이트된 열을 나타내는 **varbinary** 비트 패턴을 반환합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 또는 UPDATE 트리거의 본문 내 어디서나 `COLUMNS_UPDATED`를 사용하여 트리거에서 특정 작업을 실행해야 하는지 여부를 테스트합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COLUMNS_UPDATED ( )   
```  
  
## <a name="return-types"></a>반환 형식
**varbinary**
  
## <a name="remarks"></a>Remarks  
`COLUMNS_UPDATED`는 여러 열에서 수행되는 UPDATE 또는 INSERT 작업을 테스트하기 위한 것입니다. 한 열에 대한 UPDATE 또는 INSERT를 테스트하려면 [UPDATE()](../../t-sql/functions/update-trigger-functions-transact-sql.md)를 사용하세요.
  
`COLUMNS_UPDATED`는 왼쪽에서 오른쪽으로 정렬된 하나 이상의 바이트를 반환합니다. 각 바이트의 가장 오른쪽 비트는 최하위 비트입니다. 가장 왼쪽의 바이트에 있는 가장 오른쪽 비트는 테이블의 첫 번째 테이블 열을 나타내며, 왼쪽의 다음 비트는 두 번째 열을 나타내는 방식 등으로 이어집니다. `COLUMNS_UPDATED`는 트리거를 만든 테이블에 8개를 초과하는 열이 있는 경우 가장 왼쪽에 있는 최하위 바이트를 사용하여 여러 바이트를 반환합니다. 명시적 값 또는 암시적(NULL) 값이 삽입된 열이 있으므로 `COLUMNS_UPDATED`는 INSERT 작업의 모든 열에 대해 TRUE를 반환합니다.
  
특정 열에 대한 업데이트 또는 삽입을 테스트하려면 비트 연산자 및 테스트된 열의 정수 비트 마스크가 있는 구문을 따릅니다. 예를 들어 **t1** 테이블에 **C1**, **C2**, **C3**, **C4** 및 **C5** 열이 포함되어 있다고 가정합니다. **C2**, **C3** 및 **C4** 열이 모두 성공적으로 업데이트되었는지(**t1** 테이블에 UPDATE 트리거가 있음) 확인하려면 **& 14**가 포함된 구문을 따릅니다. **C2** 열만이 업데이트되었는지 테스트하려면 **& 2**를 지정합니다. 실제 예제는 [예제 A](https://github.com/MicrosoftDocs/sql-docs/blob/live/docs/t-sql/functions/columns-updated-transact-sql.md#a-using-columns_updated-to-test-the-first-eight-columns-of-a-table) 및 [예제 B](https://github.com/MicrosoftDocs/sql-docs/blob/live/docs/t-sql/functions/columns-updated-transact-sql.md#b-using-columns_updated-to-test-more-than-eight-columns)를 참조하세요.
  
`COLUMNS_UPDATED`는 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 또는 UPDATE 트리거 내 어디서든 사용합니다.
  
INFORMATION_SCHEMA.COLUMNS 뷰의 ORDINAL_POSITION 열은 `COLUMNS_UPDATED`에서 반환하는 열의 비트 패턴과 호환되지 않습니다. `COLUMNS_UPDATED`와 호환되는 비트 패턴을 얻으려면 다음 예제와 같이 `INFORMATION_SCHEMA.COLUMNS` 뷰를 쿼리할 때 `COLUMNPROPERTY` 시스템 함수의 `ColumnID` 속성을 참조합니다.
  
```sql
SELECT TABLE_NAME, COLUMN_NAME,  
    COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME),  
    COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
```  
  
## <a name="column-sets"></a>열 집합
테이블에 열 집합이 정의되면 `COLUMNS_UPDATED` 함수가 다음과 같은 방식으로 작동합니다.
-   열 집합의 멤버 열을 명시적으로 업데이트하는 경우, 해당 열에 대응하는 비트가 1로 설정되고 열 집합 비트가 1로 설정됩니다.  
-   열 집합을 명시적으로 업데이트하는 경우, 열 집합 비트가 1로 설정되고 해당 테이블의 모든 스파스 열에 대한 비트가 1로 설정됩니다.  
-   삽입 작업의 경우 모든 비트가 1로 설정됩니다.  
  
     열 집합이 변경되면 열 집합의 모든 열에 대한 비트가 1로 다시 설정되므로 열 집합의 변경되지 않은 열이 수정된 것으로 표시됩니다. 열 집합에 대한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-columnsupdated-to-test-the-first-eight-columns-of-a-table"></a>1. COLUMNS_UPDATED를 사용하여 테이블의 첫 번째 8개 열 테스트  
다음 예제에서는 `employeeData` 및 `auditEmployeeData`의 두 테이블을 만듭니다. `employeeData` 테이블에는 중요한 직원 급여 정보가 있으므로 인력 관리 부서의 멤버만 이를 수정할 수 있습니다. 직원의 SSN(사회 보장 번호), 연봉 또는 은행 계좌 번호가 변경되면 감사 레코드가 생성되고 `auditEmployeeData` 감사 테이블에 삽입됩니다.
  
`COLUMNS_UPDATED()` 함수를 사용하여 중요한 직원 정보가 포함된 열의 변경 내용을 빠르게 테스트할 수 있습니다. `COLUMNS_UPDATED()`를 사용하는 경우 이 방법은 테이블의 처음 8개 열에 대한 변경 내용을 검색하려고 할 때만 작동합니다.
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'employeeData')  
   DROP TABLE employeeData;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'auditEmployeeData')  
   DROP TABLE auditEmployeeData;  
GO  
CREATE TABLE dbo.employeeData (  
   emp_id int NOT NULL PRIMARY KEY,  
   emp_bankAccountNumber char (10) NOT NULL,  
   emp_salary int NOT NULL,  
   emp_SSN char (11) NOT NULL,  
   emp_lname nchar (32) NOT NULL,  
   emp_fname nchar (32) NOT NULL,  
   emp_manager int NOT NULL  
   );  
GO  
CREATE TABLE dbo.auditEmployeeData (  
   audit_log_id uniqueidentifier DEFAULT NEWID() PRIMARY KEY,  
   audit_log_type char (3) NOT NULL,  
   audit_emp_id int NOT NULL,  
   audit_emp_bankAccountNumber char (10) NULL,  
   audit_emp_salary int NULL,  
   audit_emp_SSN char (11) NULL,  
   audit_user sysname DEFAULT SUSER_SNAME(),  
   audit_changed datetime DEFAULT GETDATE()  
   );  
GO  
CREATE TRIGGER dbo.updEmployeeData   
ON dbo.employeeData   
AFTER UPDATE AS  
/* Check whether columns 2, 3 or 4 have been updated. If any or all  
columns 2, 3 or 4 have been changed, create an audit record. The
bitmask is: power(2, (2-1)) + power(2, (3-1)) + power(2, (4-1)) = 14. To test   
whether all columns 2, 3, and 4 are updated, use = 14 instead of > 0  
(below). */
  
   IF (COLUMNS_UPDATED() & 14) > 0  
/* Use IF (COLUMNS_UPDATED() & 14) = 14 to see whether all columns 2, 3,   
and 4 are updated. */  
      BEGIN  
-- Audit OLD record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'OLD',   
            del.emp_id,  
            del.emp_bankAccountNumber,  
            del.emp_salary,  
            del.emp_SSN  
         FROM deleted del;  
  
-- Audit NEW record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'NEW',  
            ins.emp_id,  
            ins.emp_bankAccountNumber,  
            ins.emp_salary,  
            ins.emp_SSN  
         FROM inserted ins;  
   END;  
GO  
  
/* Inserting a new employee does not cause the UPDATE trigger to fire. */  
INSERT INTO employeeData  
   VALUES ( 101, 'USA-987-01', 23000, 'R-M53550M', N'Mendel', N'Roland', 32);  
GO  
  
/* Updating the employee record for employee number 101 to change the   
salary to 51000 causes the UPDATE trigger to fire and an audit trail to   
be produced. */  
  
UPDATE dbo.employeeData  
   SET emp_salary = 51000  
   WHERE emp_id = 101;  
GO  
SELECT * FROM auditEmployeeData;  
GO  
  
/* Updating the employee record for employee number 101 to change both   
the bank account number and social security number (SSN) causes the   
UPDATE trigger to fire and an audit trail to be produced. */  
  
UPDATE dbo.employeeData  
   SET emp_bankAccountNumber = '133146A0', emp_SSN = 'R-M53550M'  
   WHERE emp_id = 101;  
GO  
SELECT * FROM dbo.auditEmployeeData;  
  
GO  
```  
  
### <a name="b-using-columnsupdated-to-test-more-than-eight-columns"></a>2. COLUMNS_UPDATED를 사용하여 9개 이상의 열 테스트  
처음 8개 이외의 테이블 열에 영향을 주는 업데이트를 확인하려면 `SUBSTRING` 함수를 사용하여 `COLUMNS_UPDATED`에서 정확한 비트를 반환하는지 테스트합니다. 다음 예제에서는 `AdventureWorks2012.Person.Person` 테이블의 `3`, `5` 및 `9` 열에 영향을 주는 업데이트를 테스트합니다.
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.uContact2', N'TR') IS NOT NULL  
    DROP TRIGGER Person.uContact2;  
GO  
CREATE TRIGGER Person.uContact2 ON Person.Person  
AFTER UPDATE AS  
    IF ( (SUBSTRING(COLUMNS_UPDATED(), 1, 1) & 20 = 20)   
        AND (SUBSTRING(COLUMNS_UPDATED(), 2, 1) & 1 = 1) )   
    PRINT 'Columns 3, 5 and 9 updated';  
GO  
  
UPDATE Person.Person   
   SET NameStyle = NameStyle,  
      FirstName=FirstName,  
      EmailPromotion=EmailPromotion;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:
[비트 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
[CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
[UPDATE&#40;&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)
  
  
