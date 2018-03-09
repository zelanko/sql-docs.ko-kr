---
title: SET QUOTED_IDENTIFIER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 207cf23523a315a0a4a4bc923ae9e52d7b82f8b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="set-quotedidentifier-transact-sql"></a>SET QUOTED_IDENTIFIER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 인용 부호 구분 식별자 및 리터럴 문자열에 관해 ISO 규칙을 따르도록 합니다. 큰따옴표로 구분된 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예약 키워드이거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙 구문에서 일반적으로 허용하지 않는 문자를 포함할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET QUOTED_IDENTIFIER { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET QUOTED_IDENTIFIER ON   
```  
  
## <a name="remarks"></a>주의  
 SET QUOTED_IDENTIFIER 옵션을 ON으로 설정하면 식별자를 큰따옴표로 구분할 수 있으며, 리터럴은 작은따옴표로 구분해야 합니다. SET QUOTED_IDENTIFIER 옵션을 OFF로 설정하면 식별자에 따옴표를 사용할 수 없으며 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙을 따라야 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요. 리터럴은 작은따옴표 또는 큰따옴표로 구분할 수 있습니다.  
  
 SET QUOTED_IDENTIFIER 옵션을 ON(기본값)으로 설정하면 큰따옴표로 구분된 모든 문자열이 개체 식별자로 해석됩니다. 따라서 따옴표 붙은 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙을 따르지 않아도 됩니다. 따옴표 붙은 식별자는 예약 키워드일 수 있으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자에서 일반적으로 허용되지 않는 문자를 포함할 수 있습니다. 큰따옴표로는 리터럴 문자열 식을 구분할 수 없습니다. 리터럴 문자열을 묶으려면 작은따옴표를 사용해야 합니다. 작은따옴표는 경우 (**'**) 일부인 리터럴 문자열의 두 개의 작은따옴표로 나타낼 수 있습니다 (**"**). 데이터베이스의 개체 이름에 예약된 키워드를 사용할 경우 SET QUOTED_IDENTIFIER를 ON으로 설정해야 합니다.  
  
 SET QUOTED_IDENTIFIER 옵션을 OFF로 설정하면 식의 리터럴 문자열을 작은따옴표나 큰따옴표로 구분할 수 있습니다. 리터럴 문자열을 큰따옴표로 구분할 때 아포스트로피와 같은 작은따옴표가 들어갈 수 있습니다.  
  
 계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때는 SET QUOTED_IDENTIFIER 옵션을 ON으로 설정해야 합니다. SET QUOTED_IDENTIFIER 옵션이 OFF면 계산 열에 인덱스가 있는 테이블이나 인덱싱된 뷰에서의 CREATE, UPDATE, INSERT 및 DELETE 문이 실패합니다. 계산된 열에 인덱스 및 인덱싱된 뷰에 필요한 SET 옵션 설정에 대 한 자세한 내용은 "고려 사항 때 설정 문 사용"의 참조 [SET 문 &#40; Transact SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 필터링된 인덱스를 만들 때 SET QUOTED_IDENTIFIER가 ON이어야 합니다.  
  
 XML 데이터 형식 메서드를 호출할 때는 SET QUOTED_IDENTIFIER가 ON이어야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자동으로 연결할 때 QUOTED_IDENTIFIER를 ON으로 설정 합니다. ODBC 데이터 원본과 ODBC 연결 특성 또는 OLE DB 연결 특성에서 이 옵션을 구성할 수 있습니다. DB-Library 응용 프로그램에서 연결하려면 SET QUOTED_IDENTIFIER의 기본값이 OFF여야 합니다.  
  
 테이블이 생성될 때 QUOTED IDENTIFIER 옵션이 OFF로 설정되어 있는 경우에도 해당 테이블의 메타데이터에는 항상 ON으로 저장됩니다.  
  
 저장 프로시저를 만들 때 SET QUOTED_IDENTIFIER와 SET ANSI_NULLS 설정이 캡처되어 이후에 이 저장 프로시저를 호출할 때 사용됩니다.  
  
 저장 프로시저 내에서 실행할 때는 SET QUOTED_IDENTIFIER 설정이 변경되지 않습니다.  
  
 SET ANSI_DEFAULTS 옵션을 ON으로 설정하면 SET QUOTED_IDENTIFIER가 설정됩니다.  
  
 또한 SET QUOTED_IDENTIFIER는 ALTER DATABASE의 QUOTED_IDENTIFIER 설정에 해당합니다. 데이터베이스 설정에 대 한 자세한 내용은 참조 [ALTER database&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 SET QUOTED_IDENTIFIER 구문 분석 시 효과가 이며 구문 분석 하지 쿼리 실행만 영향을 줍니다.  
  
 최상위 애드혹에 대 한 일괄 처리 구문 분석을 시작 QUOTED_IDENTIFIER에 대 한 세션의 현재 설정을 사용 합니다.  일괄 처리를 구문 분석 하는 대로 SET QUOTED_IDENTIFIER의 모든 항목, 해당 시점에서 구문 분석 동작을 변경 하 고 세션에 대 한 해당 설정을 저장 됩니다.  따라서 일괄 처리 구문 분석 되 고, 실행, 세션의 QUOTED_IDENTIFER 설정 일괄 처리에서 SET QUOTED_IDENTIFIER의 마지막 항목에 따라 설정 됩니다.  
 저장된 프로시저에서 정적 SQL 적용 생성 되거나 저장된 프로시저를 변경 하는 일괄 처리에 대 한 QUOTED_IDENTIFIER 설정을 사용 하 여 구문 분석 됩니다.  SET QUOTED_IDENTIFIER 정적 SQL 저장된 프로시저의 본문에 표시 되 면 아무 효과가 없습니다.  
  
 Sp_executesql 또는 exec ()를 사용 하 여 중첩 된 일괄 처리에 대 한 구문 분석 하는 사용 하 여 시작 된 세션의 QUOTED_IDENTIFIER 설정입니다.  중첩 된 일괄 처리 구문 분석 하는 저장 프로시저는 저장된 프로시저의 QUOTED_IDENTIFIER 설정을 사용 하 여 시작 됩니다.  중첩 된 일괄 처리를 구문 분석 하는 대로 SET QUOTED_IDENTIFIER의 모든 항목은, 해당 시점에서 구문 분석 동작을 변경 하지만 세션의 QUOTED_IDENTIFIER 설정이 업데이트 되지 않습니다.  
  
 대괄호를 사용 하 여 **[** 및 **]**식별자를 구분 하는 QUOTED_IDENTIFIER 설정에 의해 영향을 받지 않습니다.  
  
 이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```  
DECLARE @QUOTED_IDENTIFIER VARCHAR(3) = 'OFF';  
IF ( (256 & @@OPTIONS) = 256 ) SET @QUOTED_IDENTIFIER = 'ON';  
SELECT @QUOTED_IDENTIFIER AS QUOTED_IDENTIFIER;  
  
```  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-quoted-identifier-setting-and-reserved-word-object-names"></a>1. 따옴표 붙은 식별자 설정 및 예약 키워드 개체 이름 사용  
 다음 예에서는 `SET QUOTED_IDENTIFIER` 옵션을 `ON`으로 설정하고 테이블 이름의 키워드를 큰따옴표로 묶어 예약 키워드 이름이 있는 개체를 생성 및 사용합니다.  
  
```  
SET QUOTED_IDENTIFIER OFF  
GO  
-- An attempt to create a table with a reserved keyword as a name  
-- should fail.  
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);  
GO  
  
SET QUOTED_IDENTIFIER ON;  
GO  
  
-- Will succeed.  
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
  
### <a name="b-using-the-quoted-identifier-setting-with-single-and-double-quotation-marks"></a>2. 작은따옴표 및 큰따옴표를 사용해 따옴표 붙은 식별자 설정 사용  
 다음 예에서는 `SET QUOTED_IDENTIFIER` 옵션이 `ON`과 `OFF`로 설정된 문자열 식에서 작은따옴표 및 큰따옴표가 사용되는 방법을 보여 줍니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [sp_rename&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)  
  
  
