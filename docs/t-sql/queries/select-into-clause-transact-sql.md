---
title: "INTO 절(Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTO_TSQL
- INSERT_INTO_TSQL
- INSERT INTO
- INTO
- INTO clause
- INTO_clause_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- copying data [SQL Server], into a new table
- INTO clause
- moving data, to a new table
- table creation [SQL Server], INTO clause
- SELECT INTO statement
- inserting rows
- clauses [SQL Server], INTO
- row additions [SQL Server], INTO clause
ms.assetid: b48d69e8-5a00-48bf-b2f3-19278a72dd88
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 410e71466944f1744d0c8092f0ad030ffa1da29b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="select---into-clause-transact-sql"></a>SELECT - INTO 절(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SELECT INTO는 기본 파일 그룹에 새 테이블을 만든 후 쿼리의 결과 행을 이 테이블에 삽입합니다. 전체 SELECT 구문을 보려면 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
[ INTO new_table ]
[ ON filegroup]
```  
  
## <a name="arguments"></a>인수  
 *new_table*  
 선택 목록에 있는 열과 데이터 원본에서 선택한 행을 기반으로 만들려는 새 테이블의 이름을 지정합니다.  
 
  *filegroup*
 
 새 테이블을 만들 파일 그룹의 이름을 지정합니다. 지정한 파일 그룹이 데이터베이스에 있어야 합니다. 그렇지 않으면 SQL Server 엔진에서 오류를 throw합니다. 이 옵션은 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]로 시작하는 경우에만 지원됩니다.
 
 *new_table*의 형식은 선택 목록의 식을 평가하여 결정됩니다. *new_table*의 열은 선택 목록에서 지정한 순서대로 만들어집니다. *new_table*의 각 열은 선택 목록에 있는 해당 식의 이름, 데이터 형식, Null 허용 여부 및 값과 동일합니다. 열의 IDENTITY 속성은 주의 섹션의 "ID 열 작업"에 정의된 경우를 제외하고는 전송됩니다.  
  
 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 다른 데이터베이스에 테이블을 만들려면 *new_table*을 *database.schema.table_name* 형식의 정규화된 이름으로 지정합니다.  
  
 원격 서버에는 *new_table*을 만들 수 없지만, 원격 데이터 원본에서 *new_table*을 채울 수 있습니다. 원격 원본 테이블에서 *new_table*을 만들려면 네 부분으로 구성된 *linked_server*.*catalog*.*schema*.*object* 형식의 이름을 사용하여 SELECT 문의 FROM 절에 원본 테이블을 지정합니다. 또는 FROM 절에서 [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) 함수 또는 [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 함수를 사용하여 원격 데이터 원본을 지정할 수 있습니다.  
  
## <a name="data-types"></a>데이터 형식  
 FILESTREAM 특성은 새 테이블로 전송되지 않습니다. FILESTREAM BLOB은 **varbinary(max)** BLOB으로 복사되어 새 테이블에 저장됩니다. FILESTREAM 특성이 없으면 **varbinary(max)** 데이터 형식이 2GB로 제한됩니다. FILESTREAM BLOB이 이 값을 초과하면 오류 7119가 발생하고 해당 문이 중지됩니다.  
  
 기존 ID 열을 새 테이블로 선택하여 넣을 때 다음 조건 중 만족하는 것이 없는 경우 새 열은 IDENTITY 속성을 상속합니다.  
  
-   SELECT 문은 조인을 포함합니다.  
  
-   UNION을 사용하여 여러 SELECT 문을 조인합니다.  
  
-   선택 목록에서 ID 열이 두 번 이상 나열됩니다.  
  
-   ID 열이 식의 일부입니다.  
  
-   ID 열을 원격 데이터 원본에서 가져옵니다.  
  
위의 조건 중 만족하는 것이 있으면 열은 IDENTITY 속성을 상속하지 않고 NOT NULL로 만들어집니다. 새 테이블에 ID 열이 필요한데 그러한 열을 사용할 수 없는 경우 또는 원본 ID 열과 다른 초기값이나 증가값이 필요할 경우에는 IDENTITY 함수를 사용하여 선택 목록에 열을 정의합니다. 아래에 있는 예 섹션에서 "IDENTITY 함수를 사용하여 ID 열 만들기"를 참조하세요.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 테이블 변수나 테이블 반환 매개 변수를 새 테이블로 지정할 수는 없습니다.  
  
 원본 테이블이 분할되어 있는 경우에도 SELECT...INTO를 사용하여 분할된 테이블을 만들 수 없습니다. SELECT...INTO는 원본 테이블의 파티션 구성표를 사용하지 않습니다. 대신 기본 파일 그룹에 새 테이블이 만들어집니다. 분할된 테이블에 행을 삽입하려면 먼저 분할된 테이블을 만든 다음 INSERT INTO...SELECT FROM 문을 사용해야 합니다.  
  
 원본 테이블에 정의된 인덱스, 제약 조건 및 트리거는 새 테이블로 전송되지 않으며 SELECT...INTO 문에 지정할 수도 없습니다. 이러한 개체가 필요하면 SELECT...INTO 문을 실행한 후에 개체를 만들 수 있습니다.  
  
 ORDER BY 절을 지정한다고 해서 행이 지정된 순서로 삽입되는 것은 아닙니다.  
  
 SELECT 목록에 스파스 열이 있는 경우 스파스 열 속성은 새 테이블의 열로 전송되지 않습니다. 새 테이블에 이 속성이 필요하면 SELECT...INTO 문을 실행한 후 열 정의를 변경하여 이 속성을 포함하세요.  
  
 선택 목록에 계산 열이 있으면 새 테이블의 해당 열은 계산 열이 아닙니다. 새 열의 값은 SELECT...INTO가 실행될 때 계산된 값이 됩니다.  
  
## <a name="logging-behavior"></a>로깅 동작  
 SELECT...INTO의 로깅 양은 데이터베이스에 적용되는 복구 모델에 따라 달라집니다. 단순 복구 모델 또는 대량 로그 복구 모델에서는 대량 작업이 최소 로깅됩니다. 최소 로깅으로 SELECT… INTO 문을 사용하면 테이블을 만든 후 INSERT 문을 사용하여 해당 테이블을 채우는 것보다 더 효율적일 수 있습니다. 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)을(를) 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 대상 데이터베이스에서 CREATE TABLE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-table-by-specifying-columns-from-multiple-sources"></a>1. 여러 원본에서 열을 지정하여 테이블 만들기  
 다음 예에서는 다양한 직원 관련 테이블 및 주소 관련 테이블에서 7개의 열을 선택하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `dbo.EmployeeAddresses` 테이블을 만듭니다.  
  
```sql  
SELECT c.FirstName, c.LastName, e.JobTitle, a.AddressLine1, a.City,   
    sp.Name AS [State/Province], a.PostalCode  
INTO dbo.EmployeeAddresses  
FROM Person.Person AS c  
    JOIN HumanResources.Employee AS e   
    ON e.BusinessEntityID = c.BusinessEntityID  
    JOIN Person.BusinessEntityAddress AS bea  
    ON e.BusinessEntityID = bea.BusinessEntityID  
    JOIN Person.Address AS a  
    ON bea.AddressID = a.AddressID  
    JOIN Person.StateProvince as sp   
    ON sp.StateProvinceID = a.StateProvinceID;  
GO  
```  
  
### <a name="b-inserting-rows-using-minimal-logging"></a>2. 최소 로깅을 사용하여 행 삽입  
 다음 예에서는 `dbo.NewProducts` 테이블을 만든 후 `Production.Product` 테이블의 행을 삽입합니다. 여기에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 복구 모델이 FULL로 설정되었다고 가정합니다. 최소 로깅을 사용할 수 있도록 행 삽입 전에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 복구 모델이 BULK_LOGGED로 설정되고 SELECT...INTO 문 다음에 FULL로 재설정됩니다. 이 프로세스를 통해 SELECT...INTO 문은 트랜잭션 로그에 최소 공간을 사용하여 효율적으로 수행됩니다.  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
  
SELECT * INTO dbo.NewProducts  
FROM Production.Product  
WHERE ListPrice > $25   
AND ListPrice < $100;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-creating-an-identity-column-using-the-identity-function"></a>3. IDENTITY 함수를 사용하여 ID 열 만들기  
 다음 예제에서는 IDENTITY 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 새 `Person.USAddress` 테이블에 ID 열을 만듭니다. 이렇게 하는 이유는 테이블을 정의하는 SELECT 문에 조인이 포함되어 있기 때문입니다. 조인이 포함되어 있으면 IDENTITY 속성이 새 테이블에 전송되지 않습니다. IDENTITY 함수에 지정된 초기값과 증가값은 원본 테이블 `AddressID`의 `Person.Address` 열에 있는 해당 값과 다릅니다.  
  
```sql  
-- Determine the IDENTITY status of the source column AddressID.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
  
-- Create a new table with columns from the existing table Person.Address. 
-- A new IDENTITY column is created by using the IDENTITY function.  
SELECT IDENTITY (int, 100, 5) AS AddressID,   
       a.AddressLine1, a.City, b.Name AS State, a.PostalCode  
INTO Person.USAddress   
FROM Person.Address AS a  
INNER JOIN Person.StateProvince AS b 
  ON a.StateProvinceID = b.StateProvinceID  
WHERE b.CountryRegionCode = N'US';   
  
-- Verify the IDENTITY status of the AddressID columns in both tables.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
```  
  
### <a name="d-creating-a-table-by-specifying-columns-from-a-remote-data-source"></a>4. 원격 데이터 원본에서 열을 지정하여 테이블 만들기  
 다음 예에서는 원격 데이터 원본의 로컬 서버에 새 테이블을 만드는 세 가지 방법을 보여 줍니다. 먼저 원격 데이터 원본과의 링크를 만듭니다. 그런 다음 첫 번째 SELECT...INTO 문의 FROM 절과 두 번째 SELECT...INTO 문의 OPENQUERY 함수에 연결된 서버 이름 `MyLinkServer,`를 지정합니다. 세 번째 SELECT...INTO 문에서는 연결된 서버 이름을 사용하는 대신 OPENDATASOURCE 함수를 사용하여 원격 데이터 원본을 직접 지정합니다.  
  
 **적용 대상:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```sql
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_name\instance_name'.  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  

USE AdventureWorks2012;  
GO  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.Departments  
FROM MyLinkServer.AdventureWorks2012.HumanResources.Department  
GO  
-- Use the OPENQUERY function to access the remote data source.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenQuery  
FROM OPENQUERY(MyLinkServer, 'SELECT *  
               FROM AdventureWorks2012.HumanResources.Department');   
GO  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_name\instance_name.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenDataSource  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=server_name;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department;  
GO  
```  
  
### <a name="e-import-from-an-external-table-created-with--polybase"></a>5. PolyBase로 만든 외부 테이블에서 가져오기  
 Hadoop 또는 Azure Storage의 데이터를 영구적으로 저장하기 위해 SQL Server로 가져옵니다. `SELECT INTO`를 사용하여 SQL Server의 영구 저장소에 대한 외부 테이블에서 참조하는 데이터를 가져옵니다. 먼저 대략적인 관계형 테이블을 만든 다음 두 번째 단계에서 테이블 위에 columnstore 인덱스를 만듭니다.  
  
 **적용 대상:** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 참조하세요.  
  
```sql
-- Import data for car drivers into SQL Server to do more in-depth analysis.  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
```  
### <a name="f-creating-a-new-table-as-a-copy-of-another-table-and-loading-it-a-specified-filegroup"></a>6. 다른 테이블의 복사본으로 새 테이블 만들기 및 지정된 파일 그룹에 로드
다음 예제에서는 새 테이블을 다른 테이블의 복사본으로 만들고, 이를 사용자의 기본 파일 그룹과 다른 지정된 파일 그룹에 로드하는 방법을 보여 줍니다.

 **적용 대상:** [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

```sql
ALTER DATABASE [AdventureWorksDW2016] ADD FILEGROUP FG2;
ALTER DATABASE [AdventureWorksDW2016]
ADD FILE
(
NAME='FG2_Data',
FILENAME = '/var/opt/mssql/data/AdventureWorksDW2016_Data1.mdf'
)
TO FILEGROUP FG2;
GO
SELECT *  INTO [dbo].[FactResellerSalesXL] ON FG2 from [dbo].[FactResellerSales]
```
  
## <a name="see-also"></a>참고 항목  
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SELECT 예제&#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [IDENTITY&#40;함수&#41;&#40;Transact-SQL&#41;](../../t-sql/functions/identity-function-transact-sql.md)  
  
  
