---
title: 동적 데이터 마스킹 | Microsoft 문서
description: 중요한 데이터를 권한이 없는 사용자에게 마스킹해 중요한 데이터 노출을 제한하는 동적 데이터 마스킹에 대해 알아봅니다. 이는 SQL Server의 보안을 크게 간소화할 수 있습니다.
ms.date: 05/02/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: a62f4ff9-2953-42ca-b7d8-1f8f527c4d66
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9da4fe7d516453b91ab5d60ec170431035146b6b
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496954"
---
# <a name="dynamic-data-masking"></a>동적 데이터 마스킹
[!INCLUDE [SQL Server 2016 ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

![동적 데이터 마스킹](../../relational-databases/security/media/dynamic-data-masking.png)

DDM(동적 데이터 마스킹)에서는 권한이 없는 사용자로 마스킹하여 중요한 데이터 노출을 제한합니다. 애플리케이션의 보안 설계 및 코딩을 크게 간소화하는 데 사용됩니다.  

동적 데이터 마스킹을 사용하면 고객이 애플리케이션 계층에 미치는 영향을 최소화하고 표시할 중요한 데이터의 양을 지정할 수 있게 하여 중요한 데이터에 대한 무단 액세스를 방지할 수 있습니다. 지정된 데이터베이스 필드에 DDM을 구성하여 쿼리 결과 집합의 중요한 데이터를 숨길 수 있습니다. DDM을 사용하면 데이터베이스의 데이터가 변경되지 않습니다. 동적 데이터 마스킹은 마스킹 규칙이 쿼리 결과에서 적용되므로 기존 애플리케이션과 함께 사용하기 쉽습니다. 많은 애플리케이션이 기존 쿼리를 수정하지 않고 중요한 데이터를 마스킹할 수 있습니다.

* 중앙 데이터 마스킹 정책은 데이터베이스의 중요한 필드에 직접 작동합니다.
* 중요한 데이터에 대한 액세스 권한이 있는 권한 있는 사용자 또는 역할을 지정합니다.
* DDM은 전체 마스킹 및 부분 마스킹 기능과 숫자 데이터에 대한 임의 마스크 기능을 갖추고 있습니다.
* 간단한 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 명령에서 마스크를 정의하고 관리합니다.

동적 데이터 마스킹의 목적은 중요한 데이터의 노출을 제한하여 데이터에 대한 액세스 권한이 없는 사용자가 보지 못하게 하는 것이지 데이터베이스 사용자가 데이터베이스에 직접 연결하여 중요한 데이터 조각을 노출하는 과도한 쿼리를 실행하지 못하게 하는 것은 아닙니다. 동적 데이터 마스킹은 기타 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 기능(감사, 암호화, 행 수준 보안...)에 보완적이며 데이터베이스에서 중요한 데이터의 보호를 강화하기 위해 추가적으로 이 기능을 함께 사용하는 것이 좋습니다.  
  
동적 데이터 마스킹은에서 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]에서 사용할 수 있으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 사용하여 구성됩니다.합니다. Azure Portal을 사용하여 동적 데이터 마스킹을 구성하는 방법에 대한 자세한 내용은 [SQL 데이터베이스 동적 데이터 마스킹 시작(Azure Portal)](/azure/azure-sql/database/dynamic-data-masking-overview)을 참조하세요.  
  
## <a name="defining-a-dynamic-data-mask"></a>동적 데이터 마스크 정의
 해당 열에서 데이터 난독 처리를 위해 테이블의 열에 마스킹 규칙을 정의할 수 있습니다. 네 가지 유형의 마스크를 사용할 수 있습니다.  
  
|함수|Description|예제|  
|--------------|-----------------|--------------|  
|기본값|지정된 필드의 데이터 형식에 따라 전체 마스킹.<br /><br /> 문자열 데이터 형식의 경우 필드의 크기가 4자 미만인 경우 XXXX 미만의 X를 사용합니다( **char** , **nchar** ,  **varchar** , **nvarchar** , **text** , **ntext** ).  <br /><br /> 숫자 데이터 형식의 경우 영(0) 값을 사용합니다( **bigint** , **bit** , **decimal** , **int** , **money** , **numeric** , **smallint** , **smallmoney** , **tinyint** , **float** , **real** ).<br /><br /> 날짜 및 시간 데이터 형식의 경우 01.01.1900 00:00:00.0000000( **date** , **datetime2** , **datetime** , **datetimeoffset** , **smalldatetime** , **time** )을 사용합니다.<br /><br />이진 데이터 형식의 경우 단일 바이트의 ASCII 값 0을 사용합니다( **binary** , **varbinary** , **image** ).|열 정의 구문 예제: `Phone# varchar(12) MASKED WITH (FUNCTION = 'default()') NULL`<br /><br /> 변경 구문의 예제: `ALTER COLUMN Gender ADD MASKED WITH (FUNCTION = 'default()')`|  
|Email|이메일 주소의 형식에서 이메일 주소의 첫 번째 문자와 상수 접미사 ".com"을 표시하는 마스킹 방법입니다. `aXXX@XXXX.com`.|정의 구문 예제: `Email varchar(100) MASKED WITH (FUNCTION = 'email()') NULL`<br /><br /> 변경 구문의 예제: `ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()')`|  
|임의|지정된 범위 내에서 임의 값으로 원래 값을 마스킹하기 위해 숫자 유형에서 사용할 임의 마스킹 함수입니다.|정의 구문 예제: `Account_Number bigint MASKED WITH (FUNCTION = 'random([start range], [end range])')`<br /><br /> 변경 구문의 예제: `ALTER COLUMN [Month] ADD MASKED WITH (FUNCTION = 'random(1, 12)')`|  
|사용자 지정 문자열|첫 번째 및 마지막 문자를 표시하고 가운데에 사용자 지정 안쪽 여백 문자열을 추가하는 마스킹 방법입니다. `prefix,[padding],suffix`<br /><br /> 참고: 원래 값이 너무 짧아서 전체 마스크를 완료할 수 없는 경우 접두사 또는 접미사 부분이 표시되지 않습니다.|정의 구문 예제: `FirstName varchar(100) MASKED WITH (FUNCTION = 'partial(prefix,[padding],suffix)') NULL`<br /><br /> 변경 구문의 예제: `ALTER COLUMN [Phone Number] ADD MASKED WITH (FUNCTION = 'partial(1,"XXXXXXX",0)')`<br /><br /> 추가 예제:<br /><br /> `ALTER COLUMN [Phone Number] ADD MASKED WITH (FUNCTION = 'partial(5,"XXXXXXX",0)')`|  
  
## <a name="permissions"></a>사용 권한  
 동적 데이터 마스크로 테이블을 만드는 데 특별한 권한이 필요하지 않습니다. 구성표 권한에 대한 표준 **CREATE TABLE** 및 **ALTER** 만 필요합니다.  
  
 열 마스크를 추가, 대체 또는 제거하려면 테이블에서 **ALTER ANY MASK** 권한 및 **ALTER** 권한이 필요합니다. **ALTER ANY MASK** 를 보안 책임자에게 부여하는 것이 적합합니다.  
  
 테이블에 대한 **SELECT** 권한이 있는 사용자는 테이블 데이터를 볼 수 있습니다. 마스크됨으로 정의된 열은 마스크된 데이터를 표시합니다. **UNMASK** 권한을 사용자에게 부여하여 마스킹이 정의된 열에서 마스크 해제된 데이터를 검색할 수 있게 합니다.  
  
 데이터베이스의 **CONTROL** 권한은 **ALTER ANY MASK** 와 **UNMASK** 권한을 모두 포함합니다.  
  
## <a name="best-practices-and-common-use-cases"></a>최선의 구현 방법 및 일반적인 사용 사례  
  
-   열에서 마스크를 만들어도 해당 열에 대한 업데이트가 방해되지는 않습니다. 따라서 마스크된 열 쿼리 시 사용자가 마스크된 데이터를 받게 되더라도 쓰기 권한이 있는 경우 같은 사용자는 데이터를 업데이트할 수 있습니다. 업데이트 권한을 제한하려면 적절한 액세스 제어 정책을 사용해야 합니다.  
  
-   `SELECT INTO` 또는 `INSERT INTO` 을 사용하여 데이터를 마스크된 열에서 다른 테이블로 복사하면 대상 테이블에 마스크된 데이터가 생성됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 실행 시 동적 데이터 마스킹이 적용됩니다. 마스킹된 열을 포함한 데이터베이스를 사용하면 마스킹된 데이터가 있는 내보내는 데이터 파일이 생성되며( **UNMASK** 권한이 없는 사용자가 내보낸다고 가정), 가져온 데이터베이스에는 정적으로 마스킹된 데이터가 포함됩니다.  
  
## <a name="querying-for-masked-columns"></a>마스크된 열에 대한 쿼리  
 **sys.masked_columns** 뷰를 사용하여 마스킹 함수가 적용되어 있는 테이블-열에 대해 쿼리합니다. 이 보기는 **sys.columns** 보기에서 상속됩니다. **sys.columns** 뷰의 모든 열과 열이 마스킹되었는지, 그렇다면 정의된 마스킹 함수가 무엇인지 나타내는 **is_masked** 및 **masking_function** 열을 반환합니다. 이 보기는 마스킹 함수가 적용된 열만 보여줍니다.  
  
```sql 
SELECT c.name, tbl.name as table_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.[object_id] = tbl.[object_id]  
WHERE is_masked = 1;  
```  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 다음 열 형식에 대해 마스킹 규칙을 정의할 수 없습니다.  
  
-   암호화된 열(상시 암호화)  
  
-   FILESTREAM  
  
-   COLUMN_SET 또는 열 집합에 포함된 스파스 열  
  
-   계산된 열에서는 마스크를 구성할 수 없지만, 계산된 열이 MASK가 포함된 열에 종속되어 있다면 계산된 열은 마스크된 데이터를 반환합니다.  
  
-   데이터 마스킹이 있는 열은 FULLTEXT 인덱스에 대한 키가 될 수 없습니다.  
  
 **UNMASK** 권한이 없는 사용자의 경우, 사용되지 않은 **READTEXT** , **UPDATETEXT** 및 **WRITETEXT** 문은 동적 데이터 마스킹용으로 구성된 열에서 제대로 작동하지 않습니다. 
 
 동적 데이터 마스크 추가는 기본 테이블에 대한 스키마 변경으로 구현되므로 종속성이 있는 열에서 수행할 수 없습니다. 이 제한을 해결하려면 먼저 종속성을 제거하고 동적 데이터 마스크를 추가한 다음 종속성을 다시 만들면 됩니다. 예를 들어 해당 열에 종속된 인덱스로 인해 종속성이 있는 경우 해당 인덱스를 삭제하고 마스크를 추가한 다음 종속 인덱스를 다시 만들면 됩니다.
 

## <a name="security-note-bypassing-masking-using-inference-or-brute-force-techniques"></a>보안 정보: 유추 또는 무작위 기술을 사용하여 마스킹 무시

동적 데이터 마스킹은 애플리케이션에서 사용되는 미리 정의된 쿼리 집합에서 데이터 노출을 제한하여 애플리케이션 개발을 간소화하도록 설계되었습니다. 동적 데이터 마스킹은 프로덕션 데이터베이스에 직접 액세스하는 경우 중요한 데이터를 실수로 노출하지 않도록 하는 데 유용할 수 있지만, 임시 쿼리 권한이 있는 권한 없는 사용자가 기술을 사용하여 실제 데이터에 액세스할 수 있음을 알고 있어야 합니다. 이러한 임시 액세스 권한을 부여해야 하는 경우 모든 데이터베이스 작업을 모니터링하여 이 시나리오를 방지할 수 있도록 감사를 사용해야 합니다.
 
예를 들어 데이터베이스에서 임시 쿼리를 실행할 수 있는 충분한 권한이 부여된 데이터베이스 보안 주체가 있고 기본 데이터를 '추측'하여 궁극적으로 실제 값을 유추 하려 한다고 생각하고 `[Employee].[Salary]` 열에 마스크를 정의하고 이 사용자가 직접 데이터베이스에 연결하여 값 추측을 시작하면서 결국 직원의 `[Salary]` 값을 유추한다고 가정해보겠습니다.
 

```sql
SELECT ID, Name, Salary FROM Employees
WHERE Salary > 99999 and Salary < 100001;
```

>    |  Id | Name| 급여 |   
>    | ----- | ---------- | ------ | 
>    |  62543 | Jane Doe | 0 | 
>    |  91245 | John Smith | 0 |  

이 경우 임시 쿼리를 실행하는 사용자로부터 중요한 데이터를 보호하기 위해 격리 수단으로 동적 데이터 마스킹을 사용할 수 없음을 보여 줍니다. 실수로 중요한 데이터의 노출을 방지하는 데 적절하지만 악의적인 의도를 가지고 기본 데이터를 유추하는 상황은 보호되지 않습니다.
 
데이터베이스에 대한 권한을 제대로 관리하고 항상 필요한 최소 권한 원칙에 따르는 것이 중요합니다. 또한 감사를 사용하도록 설정하여 데이터베이스에서 수행하는 모든 활동을 추적해야 합니다.

  
## <a name="examples"></a>예제  
  
### <a name="creating-a-dynamic-data-mask"></a>동적 데이터 마스크 만들기  
 다음 예에서는 세 가지 유형의 동적 데이터 마스크가 있는 테이블을 만듭니다. 이 예제는 테이블을 채우며 결과를 표시하도록 선택합니다.  
  
```sql
CREATE TABLE Membership  
  (MemberID int IDENTITY PRIMARY KEY,  
   FirstName varchar(100) MASKED WITH (FUNCTION = 'partial(1,"XXXXXXX",0)') NULL,  
   LastName varchar(100) NOT NULL,  
   Phone varchar(12) MASKED WITH (FUNCTION = 'default()') NULL,  
   Email varchar(100) MASKED WITH (FUNCTION = 'email()') NULL);  
  
INSERT Membership (FirstName, LastName, Phone, Email) VALUES   
('Roberto', 'Tamburello', '555.123.4567', 'RTamburello@contoso.com'),  
('Janice', 'Galvin', '555.123.4568', 'JGalvin@contoso.com.co'),  
('Zheng', 'Mu', '555.123.4569', 'ZMu@contoso.net');  
SELECT * FROM Membership;  
```  
  
 새 사용자를 만들고 테이블에 대한 **SELECT** 권한이 부여됩니다. `TestUser` 보기가 데이터를 마스크할 때 쿼리가 실행됩니다.  
  
```sql 
CREATE USER TestUser WITHOUT LOGIN;  
GRANT SELECT ON Membership TO TestUser;  
  
EXECUTE AS USER = 'TestUser';  
SELECT * FROM Membership;  
REVERT;  
```  
  
 그 결과는 데이터를 변경하여 마스크를 보여 줍니다.  
  
 `1    Roberto     Tamburello    555.123.4567    RTamburello@contoso.com`  
  
 into  
  
 `1    RXXXXXXX    Tamburello    xxxx            RXXX@XXXX.com`  
  
### <a name="adding-or-editing-a-mask-on-an-existing-column"></a>기존 열에 대한 마스크 추가 또는 편집  
 **ALTER TABLE** 문을 사용하여 테이블의 기존 열에 마스크를 추가하거나 해당 열의 마스크를 편집합니다.  
다음 예제는 `LastName` 열에서 마스킹 함수를 추가합니다.  
  
```sql  
ALTER TABLE Membership  
ALTER COLUMN LastName ADD MASKED WITH (FUNCTION = 'partial(2,"XXX",0)');  
```  
  
 다음 예제는 `LastName` 열에서 마스킹 함수를 변경합니다.  

```sql  
ALTER TABLE Membership  
ALTER COLUMN LastName varchar(100) MASKED WITH (FUNCTION = 'default()');  
```  
  
### <a name="granting-permissions-to-view-unmasked-data"></a>마스크 해제된 데이터를 볼 수 있는 권한 부여  
 **UNMASK** 권한을 부여하면 `TestUser` 에서 마스크 해제된 데이터를 볼 수 있습니다.  
  
```sql
GRANT UNMASK TO TestUser;  
EXECUTE AS USER = 'TestUser';  
SELECT * FROM Membership;  
REVERT;   
  
-- Removing the UNMASK permission  
REVOKE UNMASK TO TestUser;  
```  
  
### <a name="dropping-a-dynamic-data-mask"></a>동적 데이터 마스크 삭제  
 다음 문은 이전 예제에서 만들 `LastName` 열에서 마스크를 삭제합니다.  
  
```sql  
ALTER TABLE Membership   
ALTER COLUMN LastName DROP MASKED;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_definition&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-definition-transact-sql.md)   
 [sys.masked_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-masked-columns-transact-sql.md)   
 [SQL 데이터베이스 동적 데이터 마스킹 시작(Azure Portal)](/azure/azure-sql/database/dynamic-data-masking-overview)
