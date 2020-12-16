---
description: DROP SCHEMA(Transact-SQL)
title: DROP SCHEMA(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SCHEMA
- DROP_SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting schemas
- schemas [SQL Server], removing
- DROP SCHEMA statement
- dropping schemas
- removing schemas
ms.assetid: 874aa29e-c8ad-41e4-a672-900fdc58f1f6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d953e19d178e0f88e2ef4689659e8a4ce74134ad
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465934"
---
# <a name="drop-schema-transact-sql"></a>DROP SCHEMA(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  데이터베이스에서 스키마를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP SCHEMA  [ IF EXISTS ] schema_name  
```  
  

```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
DROP SCHEMA schema_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 스키마를 조건부로 삭제합니다.  
  
 *schema_name*  
 데이터베이스 내에서 스키마를 식별하는 이름입니다.  
  
## <a name="remarks"></a>설명  
 삭제할 스키마에는 개체가 포함되지 않아야 합니다. 스키마에 개체가 포함된 경우 DROP 문이 실패합니다.  
  
 스키마 정보는 [sys.schemas](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md) 카탈로그 뷰에 표시됩니다.  
  
 **주의** [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 CONTROL 권한 또는 데이터베이스에 대한 ALTER ANY SCHEMA 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 단일 `CREATE SCHEMA` 문으로 시작합니다. 이 문은 `Sprockets`가 소유하는 `Krishna` 스키마와 `Sprockets.NineProngs` 테이블을 만든 다음 `SELECT`에게 `Anibal` 권한을 부여하고 `SELECT`에 대한 `Hung-Fu` 권한은 거부합니다.  
  
```sql  
CREATE SCHEMA Sprockets AUTHORIZATION Krishna   
    CREATE TABLE NineProngs (source INT, cost INT, partnumber INT)  
    GRANT SELECT TO Anibal   
    DENY SELECT TO [Hung-Fu];  
GO  
```  
  
 다음 문은 스키마를 삭제합니다. 스키마에 포함된 테이블을 먼저 삭제해야 합니다.  
  
```sql  
DROP TABLE Sprockets.NineProngs;  
DROP SCHEMA Sprockets;  
GO  
```  
  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SCHEMA&#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [DROP SCHEMA (Transact-SQL)](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
