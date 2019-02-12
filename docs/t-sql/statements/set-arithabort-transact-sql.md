---
title: SET ARITHABORT (Transact-SQL)| Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ARITHABORT_TSQL
- ARITHABORT
- SET ARITHABORT
- SET_ARITHABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- terminating queries
- queries [SQL Server], terminating
- overflow errors [SQL Server]
- ARITHABORT option
- divide-by-zero errors
- SET ARITHABORT statement
- ending queries [SQL Server]
- stopping queries
ms.assetid: f938a666-fdd1-4233-b97f-719f27b1a0e6
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ffe255903a397fd3bc1f36dd57cf38f17eac00ba
ms.sourcegitcommit: c4870cb5bebf9556cdb4d8b35ffcca265fb07862
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652552"
---
# <a name="set-arithabort-transact-sql"></a>SET ARITHABORT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```
-- Syntax for SQL Server and Azure SQL Database
  
SET ARITHABORT { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ARITHABORT ON
```
  
## <a name="remarks"></a>Remarks  
로그온 세션에서 ARITHABORT를 항상 ON으로 설정합니다. ARITHABORT를 OFF로 설정하면 쿼리 최적화에 부정적인 영향을 주어 성능 문제가 발생할 수 있습니다.  
  
> [!WARNING]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 기본 ARITHABORT 설정은 ON입니다. ARITHABORT를 OFF로 설정하는 클라이언트 애플리케이션에서 다른 쿼리 계획을 받아 성능이 저조한 쿼리 문제를 해결하기 어려울 수 있습니다. 즉, 같은 쿼리가 Management Studio에서는 빨리 실행되지만, 애플리케이션에서는 느리게 실행될 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]로 쿼리 문제를 해결할 때 항상 클라이언트 ARITHABORT 설정을 일치시키세요.  
  
SET ARITHABORT 및 SET ANSI WARNINGS이 ON이면 해당 오류 조건으로 인해 쿼리가 종료됩니다.  
  
SET ARITHABORT가 ON이고 SET ANSI WARNINGS가 OFF이면 해당 오류 조건으로 인해 일괄 처리가 종료됩니다. 트랜잭션에서 해당 오류가 발생하면 트랜잭션이 롤백됩니다. SET ARITHABORT가 OFF이고 해당 오류 중 하나가 발생하면 경고 메시지가 나타나고 산술 연산의 결과가 NULL입니다.  
  
SET ARITHABORT 및 SET ANSI WARNINGS이 OFF이고 해당 오류 중 하나가 발생하면 경고 메시지가 나타나고 산술 연산의 결과가 NULL입니다.  
  
> [!NOTE]  
>  SET ARITHABORT 및 SET ARITHIGNORE이 둘 다 ON이 아니면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 NULL을 반환하고 쿼리가 실행된 후 경고 메시지가 나타납니다.  
  
데이터베이스 호환성 수준이 90 이상으로 설정된 경우 ANSI_WARNINGS를 ON으로 설정하면 암시적으로 ARITHABORT가 ON으로 설정됩니다. 데이터베이스 호환성 수준이 80 이하로 설정된 경우에는 명시적으로 ARITHABORT 옵션을 ON으로 설정해야 합니다.  
  
식 평가의 경우 SET ARITHABORT가 OFF이고 INSERT, UPDATE 또는 DELETE 문에서 산술, 오버플로, 0으로 나누기 또는 도메인 오류가 나타나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 NULL 값을 삽입하거나 업데이트합니다. 대상 열이 Null 허용이 아니면 삽입이나 업데이트 동작이 실패하고 사용자에게 오류 메시지가 표시됩니다.  
  
SET ARITHABORT 또는 SET ARITHIGNORE 중 하나가 OFF이고 SET ANSI_WARNINGS가 ON이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 0으로 나누기 또는 오버플로 오류가 발생할 경우 여전히 오류 메시지를 반환합니다.  
  
SET ARITHABORT가 OFF이고 IF 문의 부울 조건을 평가하는 동안 중단 오류가 발생하면 FALSE 분기가 실행됩니다.
  
계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 변경할 경우 SET ARITHABORT는 ON이어야 합니다. SET ARITHABORT가 OFF이면 계산 열 또는 인덱싱된 열에 인덱스가 있는 테이블에서 CREATE, UPDATE, INSERT, DELETE 문이 실패합니다.
  
SET ARITHABORT는 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
SET ARITHABORT의 현재 설정을 보려면 다음 쿼리를 실행합니다.
  
```  
DECLARE @ARITHABORT VARCHAR(3) = 'OFF';  
IF ( (64 & @@OPTIONS) = 64 ) SET @ARITHABORT = 'ON';  
SELECT @ARITHABORT AS ARITHABORT;  
  
```  
  
## <a name="permissions"></a>Permissions  
**public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
다음 예에서는 `SET ARITHABORT` 설정이 있는 0으로 나누기 및 오버플로 오류를 보여 줍니다.  
  
```  
-- SET ARITHABORT  
-------------------------------------------------------------------------------  
-- Create tables t1 and t2 and insert data values.  
CREATE TABLE t1 (  
   a TINYINT,   
   b TINYINT  
);  
CREATE TABLE t2 (  
   a TINYINT  
);  
GO  
INSERT INTO t1   
VALUES (1, 0);  
INSERT INTO t1   
VALUES (255, 1);  
GO  
  
PRINT '*** SET ARITHABORT ON';  
GO  
-- SET ARITHABORT ON and testing.  
SET ARITHABORT ON;  
GO  
  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab   
FROM t1;  
GO  
  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be no data';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Truncate table t2.  
TRUNCATE TABLE t2;  
GO  
  
-- SET ARITHABORT OFF and testing.  
PRINT '*** SET ARITHABORT OFF';  
GO  
SET ARITHABORT OFF;  
GO  
  
-- This works properly.  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab    
FROM t1;  
GO  
  
-- This works as if SET ARITHABORT was ON.  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be 0 rows';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Drop tables t1 and t2.  
DROP TABLE t1;  
DROP TABLE t2;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ARITHIGNORE&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithignore-transact-sql.md)   
 [SESSIONPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
