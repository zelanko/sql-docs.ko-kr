---
title: OBJECT_SCHEMA_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_SCHEMA_NAME
- OBJECT_SCHEMA_NAME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- objects [SQL Server], names
- schemas [SQL Server], names
- displaying schema names
- database objects [SQL Server], names
- OBJECT_SCHEMA_NAME function
ms.assetid: 5ba90bb9-d045-4164-963e-e9e96c0b1e8b
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aba132353ef5ff75f8968957cb9e98f8c9e1ce45
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="objectschemaname-transact-sql"></a>OBJECT_SCHEMA_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  스키마 범위 개체에 대한 데이터베이스 개체 이름을 반환합니다. 목록이 스키마 범위 개체에 대 한 참조 [sys.objects&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
OBJECT_SCHEMA_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>인수  
 *object_id*  
 사용할 개체의 ID입니다. *object_id* 은 **int** 이며 지정된 된 데이터베이스 또는 현재 데이터베이스 컨텍스트에서 스키마 범위 개체로 간주 됩니다.  
  
 *database_id*  
 개체를 조회하려는 데이터베이스의 ID입니다. *database_id* 은 **int**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **sysname**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다. 대상 데이터베이스에서 AUTO_CLOSE 옵션을 ON으로 설정하면 함수가 데이터베이스를 엽니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자에게 개체에 대한 사용 권한이 없으면 OBJECT_SCHEMA_NAME과 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환할 수 있습니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 개체에 대한 ANY 권한이 필요합니다. 데이터베이스 ID를 지정하려면 데이터베이스에 대해 CONNECT 권한도 필요합니다. 그렇지 않으면 게스트 계정을 설정해야 합니다.  
  
## <a name="remarks"></a>주의  
 시스템 함수는 선택 목록, WHERE 절 및 식이 허용되는 모든 곳에서 사용될 수 있습니다. 자세한 내용은 참조 [식](../../t-sql/language-elements/expressions-transact-sql.md) 및 [여기서](../../t-sql/queries/where-transact-sql.md)합니다.  
  
 이 시스템 함수에서 반환하는 결과 집합에서는 현재 데이터베이스의 데이터 정렬을 사용합니다.  
  
 경우 *database_id* 를 지정 하지 않으면는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 있다고 가정 *object_id* 은 현재 데이터베이스의 컨텍스트에서 실행 됩니다. 참조 하는 쿼리는 *object_id* 다른 데이터베이스에서 NULL 또는 잘못 된 결과 반환 합니다. 예를 들어 다음 쿼리에서 현재 데이터베이스 컨텍스트는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 쿼리의 FROM 절에 지정된 데이터베이스 대신 이 데이터베이스의 지정된 개체 ID에 대한 개체 스키마 이름을 반환하려고 합니다. 따라서 잘못된 정보가 반환됩니다.  
  
```  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id)  
FROM master.sys.objects;  
  
```  
  
 다음 예에서는 `master` 함수에서 `OBJECT_SCHEMA_NAME` 데이터베이스에 대한 데이터베이스 ID를 지정하고 올바른 결과를 반환합니다.  
  
```  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-object-schema-name-and-object-name"></a>1. 개체 스키마 이름 및 개체 이름 반환  
 다음 예에서는 임시 문이나 준비된 문이 아닌 모든 캐시된 쿼리 계획에 대한 개체 스키마 이름, 개체 이름 및 SQL 텍스트를 반환합니다.  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_statement  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="b-returning-three-part-object-names"></a>2. 세 부분으로 된 개체 이름 반환  
 다음 예에서는 모든 데이터베이스의 모든 개체에 대해 `sys.dm_db_index_operational_stats` 동적 관리 뷰의 모든 다른 열과 함께 데이터베이스, 스키마 및 개체 이름을 반환합니다.  
  
```  
SELECT QUOTENAME(DB_NAME(database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_SCHEMA_NAME(object_id, database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_NAME(object_id, database_id))  
    , *   
FROM sys.dm_db_index_operational_stats(null, null, null, null);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [Object_id&#40; Transact SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [OBJECT_NAME &#40; Transact SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [보안 개체](../../relational-databases/security/securables.md)  
  
  
