---
description: OBJECT_NAME(Transact-SQL)
title: OBJECT_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_NAME
- OBJECT_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- OBJECT_NAME function
- viewing database object names
- objects [SQL Server], names
- database objects [SQL Server], names
- displaying database object names
- database objects [SQL Server]
- names [SQL Server], database objects
ms.assetid: 7d5b923f-0c3e-4af9-b39b-132807a6d5b3
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3386f37e4888ee8b0734d60d87359314a7bc9325
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459673"
---
# <a name="object_name-transact-sql"></a>OBJECT_NAME(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  스키마 범위 개체에 대한 데이터베이스 개체 이름을 반환합니다. 스키마 범위 개체 목록에 대해서는 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
OBJECT_NAME ( object_id [, database_id ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *object_id*  
 사용할 개체의 ID입니다. *object_id*는 **int**이며 지정한 데이터베이스 또는 현재 데이터베이스 컨텍스트에서 스키마 범위 개체로 간주됩니다.  
  
 *database_id*  
 개체를 조회하려는 데이터베이스의 ID입니다. *database_id*는 **int**입니다.  
  
## <a name="return-types"></a>반환 형식  
 **sysname**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다. 대상 데이터베이스에서 AUTO_CLOSE 옵션을 ON으로 설정하면 함수가 데이터베이스를 엽니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 OBJECT_NAME과 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 개체에 대한 ANY 권한이 필요합니다. 데이터베이스 ID를 지정하려면 데이터베이스에 대해 CONNECT 권한도 필요합니다. 그렇지 않으면 게스트 계정을 설정해야 합니다.  
  
## <a name="remarks"></a>설명  
 시스템 함수는 선택 목록, WHERE 절 및 식이 허용되는 모든 곳에서 사용될 수 있습니다. 자세한 내용은 [식](../../t-sql/language-elements/expressions-transact-sql.md) 및 [WHERE](../../t-sql/queries/where-transact-sql.md)를 참조하세요.  
  
 이 시스템 함수에서 반환하는 값에서는 현재 데이터베이스의 데이터 정렬을 사용합니다.  
  
 기본적으로 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 *object_id*가 현재 데이터베이스 컨텍스트에 있다고 간주합니다. 다른 데이터베이스의 *object_id*를 참조하는 쿼리는 NULL 또는 잘못된 결과를 반환합니다. 예를 들어 다음 쿼리에서 현재 데이터베이스 컨텍스트는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 쿼리의 FROM 절에 지정된 데이터베이스 대신 이 데이터베이스에 지정된 개체 ID의 개체 이름을 반환하려고 시도합니다. 따라서 잘못된 정보가 반환됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_NAME(object_id)  
FROM master.sys.objects;  
GO  
```  
  
 데이터베이스 ID를 지정하여 다른 데이터베이스의 컨텍스트에서 개체 이름을 확인할 수 있습니다. 다음 예에서는 `master` 함수에서 `OBJECT_SCHEMA_NAME` 데이터베이스에 대한 데이터베이스 ID를 지정하고 올바른 결과를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
GO  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-using-object_name-in-a-where-clause"></a>A. WHERE 절에서 OBJECT_NAME 사용  
 다음 예에서는 `sys.objects` 문의 `OBJECT_NAME` 절에서 `WHERE`으로 지정한 개체에 대한 열을 `SELECT` 카탈로그 뷰에서 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyID INT;  
SET @MyID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product',  
    'U'));  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(@MyID);  
GO  
```  
  
### <a name="b-returning-the-object-schema-name-and-object-name"></a>B. 개체 스키마 이름 및 개체 이름 반환  
 다음 예에서는 임시 문이나 준비된 문이 아닌 모든 캐시된 쿼리 계획에 대한 개체 스키마 이름, 개체 이름 및 SQL 텍스트를 반환합니다.  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="c-returning-three-part-object-names"></a>C. 세 부분으로 된 개체 이름 반환  
 다음 예에서는 모든 데이터베이스의 모든 개체에 대해 `sys.dm_db_index_operational_stats` 동적 관리 뷰의 모든 다른 열과 함께 데이터베이스, 스키마 및 개체 이름을 반환합니다.  
  
```  
SELECT QUOTENAME(DB_NAME(database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_SCHEMA_NAME(object_id, database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_NAME(object_id, database_id))  
    , *   
FROM sys.dm_db_index_operational_stats(NULL, NULL, NULL, NULL);  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-object_name-in-a-where-clause"></a>D. WHERE 절에서 OBJECT_NAME 사용  
 다음 예에서는 `sys.objects` 문의 `OBJECT_NAME` 절에서 `WHERE`으로 지정한 개체에 대한 열을 `SELECT` 카탈로그 뷰에서 반환합니다. (개체 번호(아래 예에서 274100017)는 달라집니다.  이 예를 테스트하려면 각자의데이터베이스에서 `SELECT name, object_id FROM sys.objects;`를 실행하여 유효한 개체 번호를 조회하세요.)  
  
```  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(274100017);  
```  
  
## <a name="see-also"></a>관련 항목  
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID&#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
  
  

