---
title: OBJECT_ID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 63
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a612928c3a30b48d3dc8e1dedd4375ca564555d8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="objectid-transact-sql"></a>OBJECT_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  스키마 범위 개체의 데이터베이스 개체 ID를 반환합니다.  
  
> [!IMPORTANT]  
>  DDL 트리거와 같은 스키마 범위가 아닌 개체는 OBJECT_ID를 사용하여 쿼리할 수 없습니다. 찾을 수 없는 개체에 대 한는 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰를 적절 한 카탈로그 뷰를 쿼리하여 개체 id 번호를 가져옵니다. 예를 들어 DDL 트리거의 개체 id 번호를 반환 하려면 사용 하 여 `SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
## <a name="arguments"></a>인수  
 **'** *object_name* **'**  
 사용할 개체입니다. *object_name* 있거나 **varchar** 또는 **nvarchar**합니다. 경우 *object_name* 은 **varchar**, 암시적으로 변환 된 **nvarchar**합니다. 데이터베이스 및 스키마 이름 지정은 옵션입니다.  
  
 **'** *object_type* **'**  
 스키마 범위 개체 형식입니다. *object_type* 있거나 **varchar** 또는 **nvarchar**합니다. 경우 *object_type* 은 **varchar**, 암시적으로 변환 된 **nvarchar**합니다. 개체 유형 목록에 대 한 참조는 **형식** 열에 [sys.objects&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="exceptions"></a>예외  
 공간 인덱스의 경우 OBJECT_ID는 NULL을 반환합니다.  
  
 오류 발생 시 NULL을 반환합니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 OBJECT_ID와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>주의  
 시스템 함수의 매개 변수가 선택 사항이면 현재 데이터베이스, 호스트 컴퓨터, 서버 사용자 또는 데이터베이스 사용자를 가정합니다. 기본 제공 함수 다음에는 항상 괄호가 와야 합니다.  
  
 현재 데이터베이스가 아닌 경우 데이터베이스 이름은 임시 테이블 이름을 보다 이전 이어야는 임시 테이블 이름이 지정 된 경우 **tempdb**합니다. 예를 들면 `SELECT OBJECT_ID('tempdb..#mytemptable')`과 같습니다.  
  
 시스템 함수는 선택 목록, WHERE 절 및 식이 허용되는 모든 곳에서 사용될 수 있습니다. 자세한 내용은 참조 [식 &#40; Transact SQL &#41; ](../../t-sql/language-elements/expressions-transact-sql.md) 및 [여기서 &#40; Transact SQL &#41; ](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-object-id-for-a-specified-object"></a>1. 지정한 개체의 개체 ID 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Production.WorkOrder` 테이블에 관한 개체 ID를 반환합니다.  
  
```  
USE master;  
GO  
SELECT OBJECT_ID(N'AdventureWorks2012.Production.WorkOrder') AS 'Object ID';  
GO  
```  
  
### <a name="b-verifying-that-an-object-exists"></a>2. 개체의 존재 여부 확인  
 다음 예에서는 테이블에 개체 ID가 있는지 확인해서 지정한 테이블이 있는지 확인합니다. 테이블이 있는 경우 삭제됩니다. 테이블이 없는 경우 `DROP TABLE` 문이 실행되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'dbo.AWBuildVersion', N'U') IS NOT NULL  
DROP TABLE dbo.AWBuildVersion;  
GO  
```  
  
### <a name="c-using-objectid-to-specify-the-value-of-a-system-function-parameter"></a>3. OBJECT_ID 사용하여 시스템 함수 매개 변수의 값을 지정  
 다음 예에서는 모든 인덱스 및 파티션에 대 한 정보를 반환 합니다.는 `Person.Address` 테이블에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 사용 하 여 데이터베이스의 [sys.dm_db_index_operational_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md) 함수입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 DB_ID 및 OBJECT_ID를 사용하여 매개 변수 값이 반환된 경우 유효한 ID가 반환되는지 항상 확인합니다. 존재하지 않는 이름을 입력하거나 철자를 잘못 입력하는 등의 이유로 데이터베이스 또는 개체 이름을 찾을 수 없으면 두 함수 모두 NULL을 반환합니다. **sys.dm_db_index_operational_stats** 함수는 NULL을 모든 데이터베이스나 모든 개체를 지정 하는 와일드 카드 값으로 해석 합니다. 이는 의도하지 않은 결과일 수 있으므로 이 섹션의 예에서는 안전하게 데이터베이스 및 개체 ID를 확인하는 방법을 보여 줍니다.  
  
```  
DECLARE @db_id int;  
DECLARE @object_id int;  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D:에 지정된 된 개체에 대 한 개체 ID 반환  
 다음 예에서는 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스의 `FactFinance` 테이블에 관한 개체 ID를 반환합니다.  
  
```  
SELECT OBJECT_ID(AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.objects &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.dm_db_index_operational_stats&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_NAME &#40; Transact SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  


