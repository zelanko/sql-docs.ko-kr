---
description: OBJECT_ID(Transact-SQL)
title: OBJECT_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_ID
- OBJECT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], IDs
- identification numbers [SQL Server], database objects
- checking object exists
- IDs [SQL Server], database objects
- OBJECT_ID function
- database objects [SQL Server], IDs
- displaying object IDs
- viewing object IDs
- verifying object exists
ms.assetid: f89286db-440f-4218-a828-30881ce3077a
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 65161cafb2ef12e2de120b0e0bd402b722447620
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670916"
---
# <a name="object_id-transact-sql"></a>OBJECT_ID(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  스키마 범위 개체의 데이터베이스 개체 ID를 반환합니다.  
  
> [!IMPORTANT]  
>  DDL 트리거와 같은 스키마 범위가 아닌 개체는 OBJECT_ID를 사용하여 쿼리할 수 없습니다. [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰에 없는 개체의 경우 해당 카탈로그 뷰를 쿼리하여 개체 ID 번호를 가져옵니다. 예를 들어 DDL 트리거의 개체 ID 번호를 반환하려면 `SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`를 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 **'** *object_name* **'**  
 사용할 개체입니다. *object_name*은 **varchar** 또는 **nvarchar**입니다. *object_name*이 **varchar**인 경우 암시적으로 **nvarchar**로 변환됩니다. 데이터베이스 및 스키마 이름 지정은 옵션입니다.  
  
 **'** *object_type* **'**  
 스키마 범위 개체 형식입니다. *object_type*은 **varchar** 또는 **nvarchar**입니다. *object_type*이 **varchar**인 경우 암시적으로 **nvarchar**로 변환됩니다. 개체 형식의 목록은 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)의 **type** 열을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="exceptions"></a>예외  
 공간 인덱스의 경우 OBJECT_ID는 NULL을 반환합니다.  
  
 오류 발생 시 NULL을 반환합니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 OBJECT_ID와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>설명  
 시스템 함수의 매개 변수가 선택 사항이면 현재 데이터베이스, 호스트 컴퓨터, 서버 사용자 또는 데이터베이스 사용자를 가정합니다. 기본 제공 함수 다음에는 항상 괄호가 와야 합니다.  
  
 임시 테이블 이름이 지정된 경우 현재 데이터베이스가 **tempdb**가 아니면 데이터베이스 이름이 임시 테이블 이름 앞에 와야 합니다. 예: `SELECT OBJECT_ID('tempdb..#mytemptable')`  
  
 시스템 함수는 선택 목록, WHERE 절 및 식이 허용되는 모든 곳에서 사용될 수 있습니다. 자세한 내용은 [식 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md) 및 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-object-id-for-a-specified-object"></a>A. 지정한 개체의 개체 ID 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Production.WorkOrder` 테이블에 관한 개체 ID를 반환합니다.  
  
```sql  
USE master;  
GO  
SELECT OBJECT_ID(N'AdventureWorks2012.Production.WorkOrder') AS 'Object ID';  
GO  
```  
  
### <a name="b-verifying-that-an-object-exists"></a>B. 개체의 존재 여부 확인  
 다음 예에서는 테이블에 개체 ID가 있는지 확인해서 지정한 테이블이 있는지 확인합니다. 테이블이 있는 경우 삭제됩니다. 테이블이 없는 경우 `DROP TABLE` 문이 실행되지 않습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'dbo.AWBuildVersion', N'U') IS NOT NULL  
DROP TABLE dbo.AWBuildVersion;  
GO  
```  
  
### <a name="c-using-object_id-to-specify-the-value-of-a-system-function-parameter"></a>C. OBJECT_ID 사용하여 시스템 함수 매개 변수의 값을 지정  
 다음 예제에서는 [sys.dm_db_index_operational_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md) 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Person.Address` 테이블의 모든 인덱스와 파티션에 대한 정보를 반환합니다.  
 
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
> [!IMPORTANT]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 DB_ID 및 OBJECT_ID를 사용하여 매개 변수 값이 반환된 경우 유효한 ID가 반환되는지 항상 확인합니다. 존재하지 않는 이름을 입력하거나 철자를 잘못 입력하는 등의 이유로 데이터베이스 또는 개체 이름을 찾을 수 없으면 두 함수 모두 NULL을 반환합니다. **sys.dm_db_index_operational_stats** 함수는 NULL을 모든 데이터베이스나 모든 개체를 지정하는 와일드카드 값으로 해석합니다. 이는 의도하지 않은 결과일 수 있으므로 이 섹션의 예에서는 안전하게 데이터베이스 및 개체 ID를 확인하는 방법을 보여 줍니다.
  
```sql  
DECLARE @db_id INT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D: 지정한 개체에 대한 개체 ID 반환  
 다음 예에서는 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스의 `FactFinance` 테이블에 관한 개체 ID를 반환합니다.  
  
```sql  
SELECT OBJECT_ID('AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>참고 항목  
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  

