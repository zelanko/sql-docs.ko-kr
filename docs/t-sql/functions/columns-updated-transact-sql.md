---
title: COLUMNS_UPDATED (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a64b20ce0d429ccd257c178abdb7c04630e409ec
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="columnsupdated-transact-sql"></a>COLUMNS_UPDATED(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **varbinary** 테이블이 나 뷰를 삽입 또는 업데이트 된 열을 나타내는 비트 패턴입니다. COLUMNS_UPDATED는 트리거가 특정 동작을 실행해야 할지 여부를 테스트하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 또는 UPDATE 트리거의 본문 내 어느 곳에서나 사용됩니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COLUMNS_UPDATED ( )   
```  
  
## <a name="return-types"></a>반환 형식
**varbinary**
  
## <a name="remarks"></a>주의  
COLUMNS_UPDATED는 여러 열을 대상으로 수행되는 UPDATE 또는 INSERT 동작을 테스트하기 위한 것입니다. 특정 열에 대 한 업데이트 또는 삽입 시도 대 한을 테스트 하려면 [update ()](../../t-sql/functions/update-trigger-functions-transact-sql.md)합니다.
  
COLUMNS_UPDATED는 왼쪽에서 오른쪽으로 정렬된 하나 이상의 바이트를 반환하며 각 바이트에서는 최하위 비트(가장 낮은 자릿수에 해당하는 비트)가 가장 오른쪽에 위치합니다. 가장 왼쪽에 있는 바이트의 가장 오른쪽 비트는 테이블의 첫 번째 열을 나타내며 그 다음 왼쪽의 비트는 두 번째 열을, 그 다음도 같은 순서로 이어집니다. COLUMNS_UPDATED는 트리거의 기반 테이블이 8개를 초과하는 열을 포함하는 경우 여러 바이트를 반환하며 최하위 비트가 제일 왼쪽에 옵니다. INSERT 동작의 경우 열에 명시적인 값 또는 암시적인(NULL) 값이 삽입되므로 COLUMNS_UPDATED는 모든 해당 열에 대해 TRUE를 반환합니다.
  
특정 열에 대한 업데이트 또는 삽입 여부를 테스트하려면 비트 연산자의 구문과 해당 열의 정수 비트 마스크를 사용합니다. 예를 들어 테이블 **t1** 열이 포함 되어 **C1**, **C2**, **C3**, **C4**, 및 **C5** . 확인 하려면 해당 열 **C2**, **C3**, 및 **C4** 이 모두 업데이트 (테이블과 **t1** UPDATE 트리거가 있는), 구문을 사용**14 &**합니다. 유일한 여부를 테스트 하려면 열 **C2** 은 지정 업데이트 **& 2**합니다.
  
COLUMNS_UPDATED는 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 또는 UPDATE 트리거 내의 어느 곳에서든 사용할 수 있습니다.
  
INFORMATION_SCHEMA.COLUMNS 뷰의 ORDINAL_POSITION 열은 COLUMNS_UPDATED에 의해 반환된 열의 비트 패턴과 호환되지 않습니다. COLUMNS_UPDATED와 호환되는 비트 패턴을 얻으려면 다음 예와 같이 `ColumnID` 뷰를 쿼리할 때 `COLUMNPROPERTY` 시스템 함수의 `INFORMATION_SCHEMA.COLUMNS` 속성을 참조하세요.
  
```sql
SELECT TABLE_NAME, COLUMN_NAME,  
    COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME),  
    COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
```  
  
## <a name="column-sets"></a>열 집합
테이블에 열 집합이 정의되면 COLUMNS_UPDATED 함수가 다음과 같이 동작합니다.
-   열 집합의 멤버인 열이 명시적으로 업데이트되면 해당 열에 대한 비트가 1로 설정되고 열 집합에 대한 비트가 1로 설정됩니다.  
-   열 집합이 명시적으로 업데이트되면 열 집합에 대한 비트가 1로 설정되고 해당 테이블의 모든 스파스 열에 대한 비트가 1로 설정됩니다.  
-   삽입 작업의 경우 모든 비트가 1로 설정됩니다.  
  
     열 집합이 변경되면 열 집합의 모든 열에 대한 비트가 1로 설정되기 때문에 변경된 열 집합의 열은 수정된 것으로 나타납니다. 열 집합에 대한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-columnsupdated-to-test-the-first-eight-columns-of-a-table"></a>1. COLUMNS_UPDATED를 사용하여 테이블의 첫 번째 8개 열 테스트  
다음 예에서는 `employeeData`와 `auditEmployeeData`라는 두 개의 테이블을 만듭니다. `employeeData` 테이블에는 중요한 직원 급여 정보가 있으므로 인력 관리 부서의 멤버만 이를 수정할 수 있습니다. 직원의 SSN(사회 보장 번호), 연봉 또는 은행 계좌 번호가 변경되는 경우에는 감사 기록이 생성되고 `auditEmployeeData` 감사 테이블로 삽입됩니다.
  
`COLUMNS_UPDATED()`를 사용하면 중요한 직원 정보를 포함하는 열이 변경되었는지 여부를 신속하게 테스트할 수 있습니다. 이러한 방식의 `COLUMNS_UPDATED()` 사용은 테이블의 처음 8개 열에 대한 변경 사항을 감지하려는 경우에만 해당됩니다.
  
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
/*Check whether columns 2, 3 or 4 have been updated. If any or all  
columns 2, 3 or 4 have been changed, create an audit record. The
bitmask is: power(2,(2-1))+power(2,(3-1))+power(2,(4-1)) = 14. To test   
whether all columns 2, 3, and 4 are updated, use = 14 instead of >0  
(below).*/
  
   IF (COLUMNS_UPDATED() & 14) > 0  
/*Use IF (COLUMNS_UPDATED() & 14) = 14 to see whether all columns 2, 3,   
and 4 are updated.*/  
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
  
/*Inserting a new employee does not cause the UPDATE trigger to fire.*/  
INSERT INTO employeeData  
   VALUES ( 101, 'USA-987-01', 23000, 'R-M53550M', N'Mendel', N'Roland', 32);  
GO  
  
/*Updating the employee record for employee number 101 to change the   
salary to 51000 causes the UPDATE trigger to fire and an audit trail to   
be produced.*/  
  
UPDATE dbo.employeeData  
   SET emp_salary = 51000  
   WHERE emp_id = 101;  
GO  
SELECT * FROM auditEmployeeData;  
GO  
  
/*Updating the employee record for employee number 101 to change both   
the bank account number and social security number (SSN) causes the   
UPDATE trigger to fire and an audit trail to be produced.*/  
  
UPDATE dbo.employeeData  
   SET emp_bankAccountNumber = '133146A0', emp_SSN = 'R-M53550M'  
   WHERE emp_id = 101;  
GO  
SELECT * FROM dbo.auditEmployeeData;  
  
GO  
```  
  
### <a name="b-using-columnsupdated-to-test-more-than-eight-columns"></a>2. COLUMNS_UPDATED를 사용하여 9개 이상의 열 테스트  
테이블에 있는 처음 8개 이외의 열에 영향을 주는 업데이트를 확인하려면 `SUBSTRING` 함수를 사용하여 `COLUMNS_UPDATED`에 의해 정확한 비트가 반환되는지 테스트합니다. 다음 예제에서는 열에 영향을 주는 업데이트에 대 한 테스트 `3`, `5`, 및 `9` 에 `AdventureWorks2012.Person.Person` 테이블입니다.
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.uContact2', N'TR') IS NOT NULL  
    DROP TRIGGER Person.uContact2;  
GO  
CREATE TRIGGER Person.uContact2 ON Person.Person  
AFTER UPDATE AS  
    IF ( (SUBSTRING(COLUMNS_UPDATED(),1,1) & 20 = 20)   
        AND (SUBSTRING(COLUMNS_UPDATED(),2,1) & 1 = 1) )   
    PRINT 'Columns 3, 5 and 9 updated';  
GO  
  
UPDATE Person.Person   
   SET NameStyle = NameStyle,  
      FirstName=FirstName,  
      EmailPromotion=EmailPromotion;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[비트 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
[CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
[업데이트 &#40; &#41; &#40; Transact SQL &#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)
  
  
