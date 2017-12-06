---
title: SET ANSI_WARNINGS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET ANSI_WARNINGS
- ANSI_WARNINGS_TSQL
- ANSI_WARNINGS
- SET_ANSI_WARNINGS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- errors [SQL Server], ISO standard behavior
- warnings [SQL Server]
- SET ANSI_WARNINGS statement
- ANSI_WARNINGS option
ms.assetid: f82aaab0-334f-427b-89b0-de4af596b4fa
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5fc4de151ed526d8019dcdd048e369a034a0536b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="set-ansiwarnings-transact-sql"></a>SET ANSI_WARNINGS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  여러 오류 상황에 대한 ISO 표준 동작을 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문
  
```
-- Syntax for SQL Server and Azure SQL Database
  
SET ANSI_WARNINGS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_WARNINGS ON
```

## <a name="remarks"></a>주의  
 SET ANSI_WARNINGS는 다음 조건에 적용됩니다.  
  
-   ON으로 설정한 경우 SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP, COUNT 등의 집계 함수에 NULL 값이 있으면 경고 메시지가 생성됩니다. OFF로 설정한 경우에는 경고가 발생하지 않습니다.  
  
-   ON으로 설정한 경우 0으로 나누기 및 산술 오버플로 오류가 발생하면 문이 롤백되고 오류 메시지가 생성됩니다. OFF로 설정한 경우 0으로 나누기 및 산술 오버플로 오류가 발생하면 NULL 값이 반환됩니다. 0으로 나누기 또는 산술 오버플로 오류가 발생 하면 인해 null 값이 반환 될 삽입 또는 업데이트 작업을 하려고 하는 경우에 발생 한 **문자**, 유니코드, 또는 **이진** 열 길이 새 값 열의 최대 크기를 초과합니다. SET ANSI_WARNINGS 옵션이 ON이면 ISO 표준에 지정된 대로 INSERT나 UPDATE가 취소됩니다. 문자 열에 대해서는 후행 공백이, 이진 열에 대해서는 후행 NULL 값이 무시됩니다. 이 옵션이 OFF이면 열의 크기에 맞게 데이터가 잘리고 문이 성공적으로 실행됩니다.  
  
    > [!NOTE]  
    >  에서 잘림이 일어날 때는 변수와 간에 **이진** 또는 **varbinary** SET 옵션에 관계 없이 데이터를 경고 또는 오류 없이 실행 합니다.  
  
    > [!NOTE]  
    >  저장 프로시저 또는 사용자 정의 함수에 매개 변수를 전달할 때 또는 일괄 처리 문에서 변수를 선언하고 설정할 때 ANSI_WARNINGS는 인식되지 않습니다. 예를 들어, 변수로 정의 되 면 **char (3)**를 하 고 다음 값으로 설정 된 3 자 보다 큰 데이터 잘리고 정의 된 크기는 INSERT 또는 UPDATE 문이 성공 합니다.  
  
 sp_configure의 user options를 사용하여 서버의 모든 연결에 대해 ANSI_WARNINGS의 기본값을 설정할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)백업 및 복원의 기본적인 백업 미디어 관련 용어를 소개합니다.  
  
 계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 조작할 때는 SET ANSI_WARNINGS 옵션을 ON으로 설정해야 합니다. SET ANSI_WARNINGS 옵션이 OFF이면 인덱싱된 뷰나 계산 열에 인덱스가 있는 테이블에서 CREATE, UPDATE, INSERT, DELETE 문이 실패합니다. 계산된 열에 인덱스 및 인덱싱된 뷰에 필요한 SET 옵션 설정에 대 한 자세한 내용은 "고려 사항 때 설정 문 사용"의 참조 [SET 문 &#40; Transact SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 ANSI_WARNINGS 데이터베이스 옵션이 포함되어 있습니다. 이 옵션은 SET ANSI_WARNINGS와 같습니다. SET ANSI_WARNINGS 옵션이 ON이면, 0으로 나누기나 데이터베이스 열에 대해 너무 큰 문자열에서 오류나 경고가 발생하고, 기타 유사한 오류가 발생합니다. SET ANSI_WARNINGS 옵션이 OFF이면 이러한 오류나 경고가 발생하지 않습니다. model 데이터베이스에서 SET ANSI_WARNINGS의 기본값은 OFF입니다. 이 옵션을 지정하지 않으면 ANSI_WARNINGS 설정이 적용됩니다. SET ANSI_WARNINGS 옵션이 OFF 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is_ansi_warnings_on 열 값을 사용 하는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰.  
  
 분산 쿼리를 실행할 때는 ANSI_WARNINGS를 ON으로 설정해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자동으로 연결할 때 ANSI_WARNINGS를 ON으로 설정 합니다. 이 옵션은 연결하기 전에 응용 프로그램에 설정된 ODBC 데이터 원본과 ODBC 연결 특성에서 구성할 수 있습니다. DB-Library 응용 프로그램으로부터 연결할 때 SET ANSI_WARNINGS의 기본값은 OFF입니다.  
  
 SET ANSI_DEFAULTS 옵션이 ON이면 SET ANSI_WARNINGS 옵션이 설정됩니다.  
  
 SET ANSI_WARNINGS 옵션은 실행 시 또는 런타임에 설정되며 구문 분석 시에는 설정되지 않습니다.  
  
 SET ARITHABORT 옵션이나 SET ARITHIGNORE 옵션 중 하나가 OFF이고 SET ANSI_WARNINGS 옵션이 ON이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 0으로 나누기 또는 오버플로 오류가 발생할 경우 여전히 오류 메시지를 반환합니다.  
  
 이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```  
DECLARE @ANSI_WARN VARCHAR(3) = 'OFF';  
IF ( (8 & @@OPTIONS) = 8 ) SET @ANSI_WARN = 'ON';  
SELECT @ANSI_WARN AS ANSI_WARNINGS;  
```  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 앞에서 언급한 대로 SET ANSI_WARNINGS 옵션이 ON과 OFF로 설정되었을 때의 세 가지 상황을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE T1   
(  
   a int,   
   b int NULL,   
   c varchar(20)  
);  
GO  
  
SET NOCOUNT ON;  
  
INSERT INTO T1   
VALUES (1, NULL, '')   
      ,(1, 0, '')  
      ,(2, 1, '')  
      ,(2, 2, '');  
  
SET NOCOUNT OFF;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS ON';  
GO  
  
SET ANSI_WARNINGS ON;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (3, 3, 'Text string longer than 20 characters');  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS OFF';  
GO  
SET ANSI_WARNINGS OFF;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (4, 4, 'Text string longer than 20 characters');  
GO  
SELECT a, b, c   
FROM T1  
WHERE a = 4;  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
DROP TABLE T1  
```  
  
## <a name="see-also"></a>관련 항목:  
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
