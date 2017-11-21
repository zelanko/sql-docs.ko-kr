---
title: SET ANSI_NULL_DFLT_OFF (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- ANSI_NULL_DFLT_OFF_TSQL
- ANSI_NULL_DFLT_OFF
- SET ANSI_NULL_DFLT_OFF
- SET_ANSI_NULL_DFLT_OFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- default nullability
- ANSI_NULL_DFLT_OFF option
- null values [SQL Server], overriding
- overriding default nullability
- SET ANSI_NULL_DFLT_OFF statement
ms.assetid: 8ed5c512-f5de-4741-a18a-de85a3041295
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1eeb95a4fdeb8e0db5ed08f3f5728a38f512bc2f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansinulldfltoff-transact-sql"></a>SET ANSI_NULL_DFLT_OFF(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스에 대 한 ANSI null 기본값 옵션이 때 새 열의 기본 null 허용 여부를 재정의 하는 세션의 동작을 변경 **true**합니다. ANSI null 기본값에 대 한 값을 설정 하는 방법에 대 한 자세한 내용은 참조 [ALTER database&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET ANSI_NULL_DFLT_OFF { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_NULL_DFLT_OFF OFF  
```  
  
## <a name="remarks"></a>주의  
 이 설정은 CREATE TABLE과 ALTER TABLE 문에 열의 Null 허용이 지정되어 있지 않을 때 새 열의 Null 허용에만 영향을 줍니다. SET ANSI_NULL_DFLT_OFF를 ON으로 설정하면 열의 Null 허용 여부 상태가 명시적으로 지정되지 않은 경우 ALTER TABLE과 CREATE TABLE 문을 사용해 만든 새 열의 기본값은 NOT NULL이 됩니다. SET ANSI_NULL_DFLT_OFF는 NULL 또는 NOT NULL을 명시적으로 지정하여 만들 열에 영향을 주지 않습니다.  
  
 SET ANSI_NULL_DFLT_OFF와 SET ANSI_NULL_DFLT_ON을 동시에 ON으로 설정할 수 없습니다. 둘 중 하나를 ON으로 설정하면 다른 옵션은 OFF로 설정됩니다. 따라서 ANSI_NULL_DFLT_OFF와 SET ANSI_NULL_DFLT_ON 중 하나만 ON으로 설정하거나 둘 다 OFF로 설정할 수 있습니다. 두 옵션 중 하나를 ON으로 설정하면 이 설정(SET ANSI_NULL_DFLT_OFF 또는 SET ANSI_NULL_DFLT_ON)이 적용됩니다. 두 옵션 모두 OFF로 설정 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is_ansi_null_default_on 열 값을 사용 하는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 Null 허용 여부 설정이 서로 다른 데이터베이스에서 사용되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트로 가장 안정적으로 작업하려면 CREATE TABLE과 ALTER TABLE 문에서 NULL 또는 NOT NULL을 항상 지정하는 것이 좋습니다.  
  
 SET ANSI_NULL_DFLT_OFF 옵션은 실행 시간이나 런타임에 설정되며 구문 분석 시간에는 설정되지 않습니다.  
  
 이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```  
DECLARE @ANSI_NULL_DFLT_OFF VARCHAR(3) = 'OFF';  
IF ( (2048 & @@OPTIONS) = 2048 ) SET @ANSI_NULL_DFLT_OFF = 'ON';  
SELECT @ANSI_NULL_DFLT_OFF AS ANSI_NULL_DFLT_OFF;  
  
```  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 ANSI Null 기본값데이터베이스 옵션에 대해 `SET ANSI_NULL_DFLT_OFF`을 두 가지 값으로 설정했을 때의 결과를 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Set the 'ANSI null default' database option to true by executing   
-- ALTER DATABASE.  
GO  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT ON;  
GO  
-- Create table t1.  
CREATE TABLE t1 (a TINYINT);  
GO  
-- NULL INSERT should succeed.  
INSERT INTO t1 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_OFF to ON and create table t2.  
SET ANSI_NULL_DFLT_OFF ON;  
GO  
CREATE TABLE t2 (a TINYINT);  
GO   
-- NULL INSERT should fail.  
INSERT INTO t2 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_OFF to OFF and create table t3.  
SET ANSI_NULL_DFLT_OFF OFF;  
GO  
CREATE TABLE t3 (a TINYINT) ;  
GO   
-- NULL INSERT should succeed.  
INSERT INTO t3 (a) VALUES (NULL);  
GO  
  
-- This illustrates the effect of having both the database  
-- option and SET option disabled.  
-- Set the 'ANSI null default' database option to false.  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT OFF;  
GO  
-- Create table t4.  
CREATE TABLE t4 (a tinyint) ;  
GO   
-- NULL INSERT should fail.  
INSERT INTO t4 (a) VALUES (null);  
GO  
  
-- SET ANSI_NULL_DFLT_OFF to ON and create table t5.  
SET ANSI_NULL_DFLT_OFF ON;  
GO  
CREATE TABLE t5 (a tinyint);  
GO   
-- NULL insert should fail.  
INSERT INTO t5 (a) VALUES (null);  
GO  
  
-- SET ANSI_NULL_DFLT_OFF to OFF and create table t6.  
SET ANSI_NULL_DFLT_OFF OFF;  
GO  
CREATE TABLE t6 (a tinyint);   
GO   
-- NULL insert should fail.  
INSERT INTO t6 (a) VALUES (null);  
GO  
  
-- Drop tables t1 through t6.  
DROP TABLE t1, t2, t3, t4, t5, t6;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40; Transact SQL &#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)  
  
  

