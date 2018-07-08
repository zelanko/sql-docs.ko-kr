---
title: 구문을 고유 하 게 컴파일된 저장된 프로시저에서 지원 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91434af003bdf783ee4f2bd2c946e4a871eac44d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37240855"
---
# <a name="supported-constructs-in-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저에서 지원되는 구문
  이 항목에서는 고유 하 게 컴파일된 저장된 프로시저에 대 한 지원 되는 기능의 목록이 포함 되어 있습니다 ([CREATE PROCEDURE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)):  
  
-   [고유 하 게 컴파일된 저장된 프로시저의 프로그래밍 기능](#pncsp)  
  
-   [지원되는 연산자](#so)  
  
-   [고유 하 게 컴파일된 저장된 프로시저의 기본 제공 함수](#bfncsp)  
  
-   [고유 하 게 컴파일된 저장된 프로시저의 쿼리 노출 영역](#qsancsp)  
  
-   [감사](#auditing)  
  
-   [테이블, 쿼리 및 조인 힌트](#tqh)  
  
-   [정렬의 제한 사항](#los)  
  
 컴파일된 저장된 프로시저를 고유 하 게 지원 되는 데이터 형식에 대 한 정보를 참조 하세요 [Supported Data Types](supported-data-types-for-in-memory-oltp.md)합니다.  
  
 지원 되지 않는 구문에 대 한 자세한 내용과 고유 하 게 컴파일된 저장된 프로시저에서 지원 되지 않는 기능 중 일부를 해결 하는 방법에 대 한 자세한 참조 [Migration Issues for Natively Compiled Stored Procedures](migration-issues-for-natively-compiled-stored-procedures.md). 지원되지 않는 기능에 대한 자세한 내용은 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](transact-sql-constructs-not-supported-by-in-memory-oltp.md)을 참조하세요.  
  
##  <a name="pncsp"></a> 고유 하 게 컴파일된 저장된 프로시저의 프로그래밍 기능  
 다음 항목이 지원됩니다.  
  
-   BEGIN ATOMIC(저장 프로시저의 외부 수준), LANGUAGE, ISOLATION LEVEL, DATEFORMAT 및 DATEFIRST  
  
-   NULL 또는 NOT NULL로 변수 선언 변수가 NOT NULL로 선언된 경우 선언에 이니셜라이저가 포함되어야 합니다. 변수가 NOT NULL로 선언되지 않은 경우 이니셜라이저는 선택 사항입니다.  
  
-   IF 및 WHILE  
  
-   INSERT/UPDATE/DELETE  
  
     하위 쿼리는 지원되지 않습니다. WHERE 또는 HAVING 절에서 AND 및 BETWEEN은 지원되고, OR, NOT 및 IN은 지원되지 않습니다.  
  
-   메모리 액세스에 최적화된 테이블 형식 및 테이블 변수  
  
-   RETURN  
  
-   SELECT  
  
-   SET  
  
-   TRY/CATCH/THROW  
  
     성능을 최적화하기 위해서는 전체 고유하게 컴파일된 저장 프로시저에 대해 단일 TRY/CATCH 블록을 사용합니다.  
  
##  <a name="so"></a> 지원되는 연산자  
 지원되는 연산자는 다음과 같습니다.  
  
-   [비교 연산자 &#40;TRANSACT-SQL&#41; ](/sql/t-sql/language-elements/comparison-operators-transact-sql) (예를 들어, >, \<, > =, 및 < =) 조건에서 지원 됩니다 (경우 동안).  
  
-   단항 연산자(+, -).  
  
-   이항 연산자(*, /, +, -, %(모듈로))  
  
     더하기 연산자(+)는 숫자 및 문자열에서 모두 지원됩니다.  
  
-   논리 연산자(AND, OR, NOT). OR 및 NOT은 IF 및 WHILE 문에서 지원되지만 WHERE 또는 HAVING 절에서는 지원되지 않습니다.  
  
-   비트 연산자 ~, &, | 및 ^  
  
##  <a name="bfncsp"></a> 고유 하 게 컴파일된 저장된 프로시저의 기본 제공 함수  
 다음 함수는 메모리 최적화 테이블에 대한 기본 제약 조건과 고유하게 컴파일된 저장 프로시저에서 지원됩니다.  
  
-   수식 함수: ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, EXP, LOG, LOG10, PI, POWER, RADIANS, RAND, SIN, SQRT, SQUARE 및 TAN  
  
-   날짜 함수: CURRENT_TIMESTAMP, DATEADD, DATEDIFF, DATEFROMPARTS, DATEPART, DATETIME2FROMPARTS, DATETIMEFROMPARTS, DAY, EOMONTH, GETDATE, GETUTCDATE, MONTH, SMALLDATETIMEFROMPARTS, SYSDATETIME, SYSUTCDATETIME 및 YEAR.  
  
-   문자열 함수: LEN, LTRIM, RTRIM 및 SUBSTRING  
  
-   ID 함수: SCOPE_IDENTITY  
  
-   NULL 함수: ISNULL  
  
-   Uniqueidentifier 함수: NEWID 및 NEWSEQUENTIALID  
  
-   오류 함수: ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY 및 ERROR_STATE  
  
-   변환: CAST 및 CONVERT. 유니코드 문자열과 유니코드가 아닌 문자열(n(var)char 및 (var)char) 간의 변환은 지원되지 않습니다.  
  
-   시스템 함수: @@rowcount 고유하게 컴파일된 저장 프로시저 내의 문은 @@rowcount를 업데이트합니다. 고유하게 컴파일된 저장 프로시저에서 @@rowcount를 사용하여 고유하게 컴파일된 저장 프로시저 내에서 실행된 마지막 문의 영향을 받는 행의 수를 확인할 수 있습니다. 그러나 @@rowcount는 고유하게 컴파일된 저장 프로시저의 실행이 시작될 때와 끝날 때 0으로 다시 설정됩니다.  
  
##  <a name="qsancsp"></a> 고유 하 게 컴파일된 저장된 프로시저의 쿼리 노출 영역  
 다음 항목이 지원됩니다.  
  
-   BETWEEN  
  
-   열 이름 별칭(AS 또는 = 구문 사용).  
  
-   SELECT 쿼리에서만 지원되는 CROSS JOIN 및 INNER JOIN  
  
-   SELECT 목록의 식이 지원 됩니다 하 고 [여기서 &#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/where-transact-sql) 절 지원 되는 연산자를 사용 하는 경우. 현재 지원되는 연산자의 목록은 [Supported Operators](#so) 를 참조하세요.  
  
-   필터 조건자 IS [NOT] NULL  
  
-   \<메모리 액세스에 최적화 된 테이블 >  
  
-   [GROUP BY &#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/select-group-by-transact-sql) AVG, COUNT, COUNT_BIG, MIN, MAX 및 SUM 집계 함수를 함께 지원 됩니다. MIN 및 MAX는 nvarchar, char, varchar, varchar, varbinary 및 binary 형식에 대해 지원되지 않습니다. [ORDER BY 절 &#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/select-order-by-clause-transact-sql) 지원 됩니다 [GROUP BY &#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/select-group-by-transact-sql) 경우에 ORDER BY 목록의 식 GROUP BY 목록에 정확 하 게 나타납니다. 예를 들어, GROUP BY a + b ORDER BY a + b는 지원되지만 GROUP BY a, b ORDER BY a + b는 지원되지 않습니다.  
  
-   HAVING(WHERE 절과 동일한 식 제한 사항이 적용됨)  
  
-   INSERT VALUES(문당 하나의 행) 및 INSERT SELECT  
  
-   ORDER BY <sup>1</sup>  
  
-   열을 참조하지 않는 조건자  
  
-   SELECT, UPDATE 및 DELETE  
  
-   상위 <sup>1</sup>  
  
-   SELECT 목록의 변수 할당.  
  
-   각 항목이 나타내는 의미는 다음과 같습니다. AND  
  
 <sup>1</sup> ORDER BY 및 TOP은 몇 가지 제한 사항이 고유 하 게 컴파일된 저장된 프로시저에서 지원 됩니다.  
  
-   에 대 한 지원은 `DISTINCT` 에 `SELECT` 또는 `ORDER BY` 절.  
  
-   `WITH TIES` 절에서는 `PERCENT` 또는 `TOP`가 지원되지 않습니다.  
  
-   `TOP` 결합할 `ORDER BY` 에서 상수를 사용할 경우 8,192 개 이상은 지원 하지 않습니다는 `TOP` 절. 쿼리에 조인 또는 집계 함수가 포함되어 있으면 이 제한이 더 낮아질 수 있습니다. 예를 들어, 조인이 하나 있고 테이블이 두 개 있으면 4,096개의 행으로 제한되고, 조인이 두 개 있고 테이블이 세 개 있으면 2,730개의 행으로 제한됩니다.  
  
     변수에 행 수를 저장하여 8,192개 이상의 결과를 가져올 수 있습니다.  
  
    ```tsql  
    DECLARE @v INT = 9000  
    SELECT TOP (@v) … FROM … ORDER BY …  
    ```  
  
 하지만 `TOP` 절에 상수를 사용하면 변수를 사용할 때보다 나은 성능을 가져옵니다.  
  
 이러한 제한 사항은 해석 된 적용 되지 않습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 메모리 최적화 테이블에 대 한 액세스.  
  
##  <a name="auditing"></a> 감사  
 프로시저 수준 감사는 고유하게 컴파일된 저장 프로시저에서 지원됩니다. 문 수준 감사는 지원되지 않습니다.  
  
 감사에 대한 자세한 내용은 [Create a Server Audit and Database Audit Specification](../security/auditing/create-a-server-audit-and-database-audit-specification.md)를 참조하세요.  
  
##  <a name="tqh"></a> 테이블, 쿼리 및 조인 힌트  
 다음 항목이 지원됩니다.  
  
-   테이블 힌트 구문 또는 쿼리의 [OPTION 절&#40;Transact-SQL&#41;](/sql/t-sql/queries/option-clause-transact-sql)에 있는 INDEX, FORCESCAN 및 FORCESEEK 힌트.  
  
-   FORCE ORDER  
  
-   INNER LOOP JOIN  
  
-   OPTIMIZE FOR  
  
 자세한 내용은 [힌트 &#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/hints-transact-sql)합니다.  
  
##  <a name="los"></a> 정렬의 제한 사항  
 [TOP&#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) 및 [ORDER BY 절&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql)을 사용하는 쿼리에서는 8,000개 이상의 행을 정렬할 수 있습니다. 하지만 [ORDER BY 절&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql)이 없을 경우, [TOP&#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql)은 최대 8,000개까지만 행을 정렬할 수 있습니다. 조인이 있으면 이러한 행 수가 더 줄어듭니다.  
  
 쿼리에서 [TOP&#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) 연산자와 [ORDER BY 절&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql)을 모두 사용하는 경우 TOP 연산자에 대해 최대 8192행을 지정할 수 있습니다. 8192행보다 더 많이 지정하면 다음 오류 메시지가 나타납니다. **메시지 41398, 수준 16, 상태 1, 프로시저 *\<procedureName>*, 줄 *\<lineNumber>* TOP 연산자는 최대 8192개의 행을 반환할 수 있습니다. *\<number>* 개가 요청되었습니다.**  
  
 TOP 절을 사용하지 않는 경우 ORDER BY를 사용하여 몇 행이든 정렬할 수 있습니다.  
  
 ORDER BY 절을 사용하지 않는 경우 TOP 연산자와 함께 어떤 정수 값이든 사용할 수 있습니다.  
  
 TOP N = 8192인 경우의 예: 컴파일  
  
```tsql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8192 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 TOP N > 8192인 경우의 예: 컴파일 실패  
  
```tsql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8193 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 8192 행 제한은 `TOP N` 에만 적용됩니다. 여기서 `N` 은 앞의 예와 같이 상수입니다.  8192보다 큰 `N` 이 필요한 경우 값을 변수에 할당하고 이 변수를 `TOP`과 함께 사용할 수 있습니다.  
  
 변수 사용의 예: 컴파일  
  
```tsql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    DECLARE @v int = 8193   
    SELECT TOP (@v) ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 **반환된 행에 대한 제한:** TOP 연산자에서 반환할 수 있는 행 수를 잠재적으로 줄일 수 있는 두 가지 경우는 다음과 같습니다.  
  
-   쿼리에서 JOIN 사용.  JOIN이 제한에 미치는 영향은 쿼리 계획에 따라 다릅니다.  
  
-   집계 함수 또는 참조를 사용하여 ORDER BY 절에서 함수 집계.  
  
 TOP N에서 지원되는 최대 N의 경우를 계산하는 공식은 `N = floor ( 65536 / number_of_tables * 8 + total_size+of+aggs )`입니다.  
  
## <a name="see-also"></a>관련 항목  
 [고유하게 컴파일된 저장 프로시저](natively-compiled-stored-procedures.md)   
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
