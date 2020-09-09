---
description: sp_rename(Transact-SQL)
title: sp_rename (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_rename_TSQL
- sp_rename
dev_langs:
- TSQL
helpviewer_keywords:
- renaming indexes
- renaming columns
- sp_rename
- renaming tables
ms.assetid: bc3548f0-143f-404e-a2e9-0a15960fc8ed
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: edfe9a3a3d69c95b2a8778ca44583e005c6495c6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538655"
---
# <a name="sp_rename-transact-sql"></a>sp_rename(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 데이터베이스에 있는 사용자가 만든 개체의 이름을 변경합니다. 이 개체는 테이블, 인덱스, 열, 별칭 데이터 형식 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR (공용 언어 런타임) 사용자 정의 형식일 수 있습니다.  
  
> [!CAUTION]  
>  개체 이름의 일부를 변경하면 스크립트나 저장 프로시저가 작동되지 않을 수 있습니다. 이 문을 사용하여 저장 프로시저, 트리거, 사용자 정의 함수 또는 뷰의 이름을 변경하지 않는 것이 좋습니다. 대신 개체를 삭제하고 새로운 이름으로 다시 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_rename [ @objname = ] 'object_name' , [ @newname = ] 'new_name'   
    [ , [ @objtype = ] 'object_type' ]   
```  
  
## <a name="arguments"></a>인수  
 [ @objname =] '*object_name*'  
 현재 사용자 개체나 데이터 형식의 정규화된 이름 또는 정규화되지 않은 이름입니다. 이름을 바꿀 개체가 테이블의 열인 경우에는 *테이블. column* 또는 *schema. table 열*에 *object_name* 있어야 합니다. 이름을 바꿀 개체가 인덱스 이면 *object_name* *테이블. index* 또는 *schema. table. index*형식 이어야 합니다. 이름을 바꿀 개체가 제약 조건이 면 *object_name* 은 *schema. 제약 조건*형식 이어야 합니다.  
  
 정규화된 개체가 지정된 경우에는 따옴표만 필요합니다. 데이터베이스 이름을 포함한 정규화된 이름인 경우 반드시 현재 데이터베이스의 이름을 사용해야 합니다. *object_name* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
 [ @newname =] '*new_name*'  
 지정한 개체의 새 이름입니다. *new_name* 은 한 부분으로 구성 된 이름 이어야 하며 식별자 규칙을 따라야 합니다. *newname* 은 **sysname**이며 기본값은 없습니다.  
  
> [!NOTE]  
>  트리거 이름은 # 또는 ##로 시작될 수 없습니다.  
  
 [ @objtype =] '*object_type*'  
 이름을 바꾸는 개체의 유형입니다. *object_type* 는 **varchar (13)** 이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|COLUMN|이름을 바꿀 열입니다.|  
|DATABASE|사용자 정의 데이터베이스입니다. 이 개체 유형은 데이터베이스 이름을 바꿀 경우 필요합니다.|  
|INDEX|사용자 정의 인덱스입니다. 통계가 포함된 인덱스의 이름을 바꾸면 통계 이름도 자동으로 바뀝니다.|  
|OBJECT|[Sys. 개체](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)에서 추적 되는 형식의 항목입니다. 예를 들어 OBJECT는 제약 조건(CHECK, FOREIGN KEY, PRIMARY/UNIQUE KEY), 사용자 테이블 및 규칙을 포함하는 개체의 이름을 바꿀 때 사용될 수 있습니다.|  
|STATISTICS|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /><br /> 사용자가 명시적으로 만들었거나 인덱스를 통해 암시적으로 만들어진 통계입니다. 인덱스의 통계 이름을 바꾸면 인덱스 자체도 자동으로 이름이 바뀝니다.|  
|USERDATATYPE|[CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) 또는 [sp_addtype](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md)를 실행 하 여 추가 된 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) 입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 수(실패)  
  
## <a name="remarks"></a>설명  
 현재 데이터베이스에서만 개체 또는 데이터 형식의 이름을 변경할 수 있습니다. 대부분의 시스템 데이터 형식 및 시스템 개체의 이름은 변경할 수 없습니다.  
  
 sp_rename은 PRIMARY KEY 또는 UNIQUE 제약 조건의 이름을 바꿀 때마다 연결된 인덱스의 이름을 자동으로 바꿉니다. 이름을 바꾼 인덱스가 PRIMARY KEY 제약 조건과 연결된 경우 PRIMARY KEY 제약 조건의 이름도 sp_rename에 의해 자동으로 바뀝니다.  
  
 sp_rename을 사용하여 기본 XML 인덱스 및 보조 XML 인덱스의 이름을 변경할 수 있습니다.  
  
 저장 프로시저, 함수, 뷰 또는 트리거의 이름을 바꾸면 [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰의 정의 열 또는 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) 기본 제공 함수를 사용 하 여 가져온 해당 개체의 이름이 변경 되지 않습니다. 따라서 이러한 개체 유형의 이름을 변경할 때 sp_rename을 사용하지 않는 것이 좋습니다. 대신 해당 개체를 삭제하고 새로운 이름으로 다시 만듭니다.  
  
 테이블이나 열과 같은 개체의 이름을 변경해도 이 개체를 참조하는 개체의 이름은 자동으로 변경되지 않습니다. 이름을 변경한 개체를 참조하는 개체는 수동으로 수정해야 합니다. 예를 들어 테이블 열의 이름을 변경하고 이 열이 트리거에서 참조되는 경우 트리거를 수정하여 새로운 열 이름을 적용해야 합니다. [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 를 사용하여 이 개체에 종속된 개체를 나열한 다음 개체의 이름을 변경할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 개체, 열 및 인덱스의 이름을 변경하려면 개체에 대한 ALTER 권한이 필요합니다. 사용자 유형의 이름을 변경하려면 유형에 대한 CONTROL 권한이 필요합니다. 데이터베이스의 이름을 변경하려면 sysadmin 또는 dbcreator 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-renaming-a-table"></a>A. 테이블 이름 바꾸기  
 다음 예에서는 `SalesTerritory` 스키마에 있는 `SalesTerr` 테이블의 이름을 `Sales` 로 바꿉니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
GO  
```  
  
### <a name="b-renaming-a-column"></a>B. 열 이름 바꾸기  
 다음 예에서는 `TerritoryID` 테이블의 열 이름을 `SalesTerritory` 로 변경 합니다 `TerrID` .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
GO  
```  
  
### <a name="c-renaming-an-index"></a>C. 인덱스 이름 바꾸기  
 다음 예에서는 `IX_ProductVendor_VendorID` 인덱스의 이름을 `IX_VendorID`로 변경합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';  
GO  
```  
  
### <a name="d-renaming-an-alias-data-type"></a>D. 별칭 데이터 형식 이름 바꾸기  
 다음 예에서는 `Phone` 별칭 데이터 형식의 이름을 `Telephone`으로 변경합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Phone', N'Telephone', N'USERDATATYPE';  
GO  
```  
  
### <a name="e-renaming-constraints"></a>E. 제약 조건 이름 바꾸기  
 다음 예에서는 PRIMARY KEY 제약 조건, CHECK 제약 조건 및 FOREIGN KEY 제약 조건의 이름을 바꿉니다. 제약 조건 이름을 바꿀 때는 제약 조건이 속한 스키마를 지정해야 합니다.  
  
```  
USE AdventureWorks2012;   
GO  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');   
GO  
  
-- Rename the primary key constraint.  
sp_rename 'HumanResources.PK_Employee_BusinessEntityID', 'PK_EmployeeID';  
GO  
  
-- Rename a check constraint.  
sp_rename 'HumanResources.CK_Employee_BirthDate', 'CK_BirthDate';  
GO  
  
-- Rename a foreign key constraint.  
sp_rename 'HumanResources.FK_Employee_Person_BusinessEntityID', 'FK_EmployeeID';  
  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');  
  
```  
  
```  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_Person_BusinessEntityID   HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_BusinessEntityID          HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_Employee_BirthDate                 HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_ID                        HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_ID                        HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_BirthDate                          HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
```  
  
### <a name="f-renaming-statistics"></a>F. 통계 이름 바꾸기  
 다음 예에서는 contactMail1 라는 통계 개체를 만든 후 sp_rename를 사용 하 여 통계의 이름을 NewContact로 바꿉니다. 통계 이름을 바꾸면 개체를 schema.table.statistics_name 형식으로 지정해야 합니다.  
  
```  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
  
sp_rename 'Person.Person.ContactMail1', 'NewContact','Statistics';  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
