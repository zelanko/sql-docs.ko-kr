---
description: SET QUOTED_IDENTIFIER(Transact-SQL)
title: SET QUOTED_IDENTIFIER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUOTED_IDENTIFIER_TSQL
- SET_QUOTED_IDENTIFIER_TSQL
- SET QUOTED_IDENTIFIER
- QUOTED_IDENTIFIER
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- identifiers [SQL Server], delimited
- QUOTED_IDENTIFIER option
- quoted identifiers
- ISO delimited identifiers rules
- SET QUOTED_IDENTIFIER statement
ms.assetid: 10f66b71-9241-4a3a-9292-455ae7252565
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b944acae465dee3d6ba30e6807d4d74e38742555
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544136"
---
# <a name="set-quoted_identifier-transact-sql"></a>SET QUOTED_IDENTIFIER(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 인용 부호 구분 식별자 및 리터럴 문자열에 관해 ISO 규칙을 따르도록 합니다. 큰따옴표로 구분된 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예약 키워드이거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙 구문에서 일반적으로 허용하지 않는 문자를 포함할 수 있습니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for SQL Server and Azure SQL Database

SET QUOTED_IDENTIFIER { ON | OFF }
```

```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET QUOTED_IDENTIFIER ON
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명
`SET QUOTED_IDENTIFIER`가 ON(기본값)이면, 식별자는 큰따옴표(“ ”)로 구분할 수 있고 리터럴은 작은따옴표(‘ ’)로 구분해야 합니다. 큰따옴표로 구분되는 모든 문자열은 개체 식별자로 해석됩니다. 따라서 따옴표 붙은 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙을 따르지 않아도 됩니다. 따옴표 붙은 식별자는 예약 키워드일 수 있으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자에서 일반적으로 허용되지 않는 문자를 포함할 수 있습니다. 큰따옴표로는 리터럴 문자열 식을 구분할 수 없습니다. 리터럴 문자열을 묶으려면 작은따옴표를 사용해야 합니다. 리터럴 문자열에 작은따옴표(‘)가 포함되어 있으면, 두 개의 작은따옴표(‘’)로 나타낼 수 있습니다. 데이터베이스의 개체 이름에 예약된 키워드를 사용하는 경우 `SET QUOTED_IDENTIFIER`를 ON으로 설정해야 합니다.

`SET QUOTED_IDENTIFIER`가 OFF이면, 식별자를 따옴표로 묶을 수 없으며 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙을 따라야 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요. 리터럴은 작은따옴표 또는 큰따옴표로 구분할 수 있습니다. 리터럴 문자열을 큰따옴표로 구분할 때 아포스트로피와 같은 작은따옴표가 들어갈 수 있습니다.

> [!NOTE]
> QUOTED_IDENTIFIER는 대괄호([ ])로 묶인 구분 식별자에 영향을 주지 않습니다.

계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우 `SET QUOTED_IDENTIFIER`를 ON으로 설정해야 합니다. `SET QUOTED_IDENTIFIER`가 OFF이면, 계산 열에 인덱스가 있는 테이블이나 인덱싱된 뷰가 있는 테이블에서 CREATE, UPDATE, INSERT, DELETE 문이 실패합니다. 계산 열의 인덱스 및 인덱싱된 뷰에 필요한 SET 옵션 설정에 대한 자세한 내용은 [SET 문 사용 시 고려 사항](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements)을 참조하세요.

필터링된 인덱스를 만드는 경우 `SET QUOTED_IDENTIFIER`를 ON으로 설정해야 합니다.

XML 데이터 형식 메서드를 호출하는 경우 `SET QUOTED_IDENTIFIER`를 ON으로 설정해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 연결할 때 QUOTED_IDENTIFIER를 자동으로 ON으로 설정합니다. ODBC 데이터 원본과 ODBC 연결 특성 또는 OLE DB 연결 특성에서 이 옵션을 구성할 수 있습니다. DB-Library 애플리케이션에서 연결하려면 SET QUOTED_IDENTIFIER의 기본값이 OFF여야 합니다.

테이블이 생성될 때 QUOTED IDENTIFIER 옵션이 OFF로 설정되어 있는 경우에도 해당 테이블의 메타데이터에는 항상 ON으로 저장됩니다.

저장 프로시저를 만들 때 SET QUOTED_IDENTIFIER와 SET ANSI_NULLS 설정이 캡처되어 이후에 이 저장 프로시저를 호출할 때 사용됩니다.

저장 프로시저 내에서 실행할 때는 SET QUOTED_IDENTIFIER 설정이 변경되지 않습니다.

`SET ANSI_DEFAULTS`가 ON이면, QUOTED_IDENTIFIER도 ON이 됩니다.

또한 `SET QUOTED_IDENTIFIER`는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)의 QUOTED_IDENTIFIER 설정에 해당합니다.

`SET QUOTED_IDENTIFIER`는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문 분석 시 적용되며, 구문 분석에만 영향을 주고 쿼리 최적화나 쿼리 실행에는 영향을 주지 않습니다.

최상위 수준의 임시 일괄 처리를 위해 QUOTED_IDENTIFIER에 대한 세션의 현재 설정을 사용하여 구문 분석을 시작합니다. 일괄 처리를 구문 분석하는 경우, 그 시점부터 발생한 `SET QUOTED_IDENTIFIER`의 구문 분석 동작이 모두 변경되고 해당 설정이 세션에 대해 저장됩니다. 따라서 일괄 처리가 구문 분석되고 실행된 후 세션의 QUOTED_IDENTIFER 설정은 일괄 처리에서 마지막으로 발생한 `SET QUOTED_IDENTIFIER`에 따라 설정됩니다.

저장 프로시저의 정적 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 저장 프로시저를 만들거나 변경한 일괄 처리에 대해 적용된 QUOTED_IDENTIFIER 설정을 사용하여 구문 분석됩니다. `SET QUOTED_IDENTIFIER`가 저장 프로시저 본문에 정적 [!INCLUDE[tsql](../../includes/tsql-md.md)]로 표시될 때는 아무 효과도 없습니다.

`sp_executesql` 또는 `exec()`를 사용하는 중첩된 일괄 처리의 경우 세션의 QUOTED_IDENTIFIER 설정을 사용하여 구문 분석이 시작됩니다. 중첩된 일괄 처리가 저장 프로시저 내부에 있는 경우 저장 프로시저의 QUOTED_IDENTIFIER 설정을 사용하여 구문 분석이 시작됩니다. 중첩된 일괄 처리를 구문 분석하는 경우, 그 시점부터 발생하는 `SET QUOTED_IDENTIFIER`의 구문 분석 동작이 모두 변경되지만 세션의 QUOTED_IDENTIFIER 설정은 업데이트되지 않습니다.

이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.

```sql
DECLARE @QUOTED_IDENTIFIER VARCHAR(3) = 'OFF';
IF ( (256 & @@OPTIONS) = 256 ) 
SET @QUOTED_IDENTIFIER = 'ON';

SELECT @QUOTED_IDENTIFIER AS QUOTED_IDENTIFIER;
```

## <a name="permissions"></a>사용 권한
`PUBLIC` 역할의 멤버 자격이 필요합니다.

## <a name="examples"></a>예

### <a name="a-using-the-quoted-identifier-setting-and-reserved-word-object-names"></a>A. 따옴표 붙은 식별자 설정 및 예약 키워드 개체 이름 사용

다음 예에서는 `SET QUOTED_IDENTIFIER` 옵션을 `ON`으로 설정하고 테이블 이름의 키워드를 큰따옴표로 묶어 예약 키워드 이름이 있는 개체를 생성 및 사용합니다.

```sql
SET QUOTED_IDENTIFIER OFF
GO

-- Create statement fails.
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);
GO

SET QUOTED_IDENTIFIER ON;
GO

-- Create statement succeeds.
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);
GO

SELECT "identity","order"
FROM "select"
ORDER BY "order";
GO

DROP TABLE "SELECT";
GO

SET QUOTED_IDENTIFIER OFF;
GO
```

### <a name="b-using-the-quoted-identifier-setting-with-single-and-double-quotation-marks"></a>B. 작은따옴표 및 큰따옴표를 사용해 따옴표 붙은 식별자 설정 사용

 다음 예에서는 `SET QUOTED_IDENTIFIER` 옵션이 `ON`과 `OFF`로 설정된 문자열 식에서 작은따옴표 및 큰따옴표가 사용되는 방법을 보여 줍니다.

```sql
SET QUOTED_IDENTIFIER OFF;
GO

USE AdventureWorks2012;
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES
    WHERE TABLE_NAME = 'Test')
    DROP TABLE dbo.Test;
GO
USE AdventureWorks2012;
CREATE TABLE dbo.Test (ID INT, String VARCHAR(30)) ;
GO

-- Literal strings can be in single or double quotation marks.
INSERT INTO dbo.Test VALUES (1, "'Text in single quotes'");
INSERT INTO dbo.Test VALUES (2, '''Text in single quotes''');
INSERT INTO dbo.Test VALUES (3, 'Text with 2 '''' single quotes');
INSERT INTO dbo.Test VALUES (4, '"Text in double quotes"');
INSERT INTO dbo.Test VALUES (5, """Text in double quotes""");
INSERT INTO dbo.Test VALUES (6, "Text with 2 """" double quotes");
GO

SET QUOTED_IDENTIFIER ON;
GO

-- Strings inside double quotation marks are now treated
-- as object names, so they cannot be used for literals.
INSERT INTO dbo."Test" VALUES (7, 'Text with a single '' quote');
GO

-- Object identifiers do not have to be in double quotation marks
-- if they are not reserved keywords.
SELECT ID, String
FROM dbo.Test;
GO

DROP TABLE dbo.Test;
GO

SET QUOTED_IDENTIFIER OFF;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
 ID          String
 ----------- ------------------------------
 1           'Text in single quotes'
 2           'Text in single quotes'
 3           Text with 2 '' single quotes
 4           "Text in double quotes"
 5           "Text in double quotes"
 6           Text with 2 "" double quotes
 7           Text with a single ' quote
 ```

## <a name="see-also"></a>참고 항목
[CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md)    
[CREATE DEFAULT](../../t-sql/statements/create-default-transact-sql.md)    
[CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)    
[CREATE RULE](../../t-sql/statements/create-rule-transact-sql.md)    
[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)    
[CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md)    
[CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)    
[데이터 형식](../../t-sql/data-types/data-types-transact-sql.md)    
[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)    
[SELECT](../../t-sql/queries/select-transact-sql.md)    
[SET 문](../../t-sql/statements/set-statements-transact-sql.md)    
[SET ANSI_DEFAULTS](../../t-sql/statements/set-ansi-defaults-transact-sql.md)    
[sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)    
[데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)
