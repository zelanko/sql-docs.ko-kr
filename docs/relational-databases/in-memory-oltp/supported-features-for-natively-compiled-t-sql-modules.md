---
title: "고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능 | Microsoft 문서"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
caps.latest.revision: 44
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 332787256518605b6f91dab6be012889c0b0aa93
ms.openlocfilehash: 0d87653d1db0ffad098e9cdf914d61a486905647
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="supported-features-for-natively-compiled-t-sql-modules"></a>고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]


  이 항목에서는 저장 프로시저([CREATE PROCEDURE(Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)), 스칼라 사용자 정의 함수, 인라인 테이블 반환 함수, 트리거 등 고유하게 컴파일된 T-SQL 모듈의 본문에서 지원되는 기능 및 T-SQL 노출 영역 목록을 제공합니다.  

 네이티브 모듈 정의와 관련하여 지원되는 기능은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 DDL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)을 참조하세요.  

-   [네이티브 모듈의 쿼리 노출 영역](#qsancsp)  

-   [데이터 수정](#dml)  

-   [흐름 제어 언어](#cof)  

-   [지원되는 연산자](#so)  

-   [고유하게 컴파일된 모듈의 기본 제공 함수](#bfncsp)  

-   [감사](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#auditing)  

-   [테이블 및 쿼리 힌트](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#tqh)  

-   [정렬의 제한 사항](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#los)  

 고유하게 컴파일된 모듈에서 지원되지 않는 구문에 대한 자세한 내용과 지원되지 않는 일부 기능을 해결하는 방법은 [Migration Issues for Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)를 참조하세요. 지원되지 않는 기능에 대한 자세한 내용은 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)을 참조하세요.  

##  <a name="qsancsp"></a> 네이티브 모듈의 쿼리 노출 영역  

다음과 같은 쿼리 구문이 지원됩니다.  

CASE 식: 모든 문이나 절 유효한 식을 허용 하는 대/소문자를 사용할 수 있습니다.
   - **적용 대상:** [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]합니다.  
    부터는 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], CASE 문은 고유 하 게 컴파일된 T-SQL 모듈에 대 한 이제 지원 됩니다.

SELECT 절:  

-   열 및 이름 별칭(AS 또는 = 구문 사용)  

-   스칼라 하위 쿼리
    - **적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]합니다.
      부터는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], 스칼라 하위 쿼리는 이제 네이티브 컴파일된 모듈에서 지원 됩니다.

-   TOP*  

-   SELECT DISTINCT  
    - **적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]합니다.
      부터는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], DISTINCT 연산자 고유 하 게 컴파일된 모듈에서 지원 됩니다.

              DISTINCT aggregates are not supported.  

-   UNION 및 UNION ALL
    - **적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]합니다.
      부터는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], UNION 및 UNION ALL 연산자가 이제 고유 하 게 컴파일된 모듈에서 지원 됩니다.

-   변수 할당  

FROM 절:  

-   FROM \<메모리 액세스에 최적화된 테이블 또는 테이블 변수>  

-   FROM \<고유하게 컴파일된 인라인 TVF>  

-   LEFT OUTER JOIN, RIGHT OUTER JOIN, CROSS JOIN 및 INNER JOIN
    - **적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]합니다.
      부터는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], 조인 이제 네이티브 컴파일된 모듈에서 지원 됩니다.

-   하위 쿼리 `[AS] table_alias`. 자세한 내용은 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)을 참조하세요. 
    - **적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]합니다.
      부터는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], 하위 쿼리는 이제 네이티브 컴파일된 모듈에서 지원 됩니다.

WHERE 절:  

-   필터 조건자 IS [NOT] NULL  

-   및 사이  
-   OR, NOT, EXISTS,
    - **적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]합니다.
      부터는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], OR/NOT/IN/EXISTS 연산자는 이제 네이티브 컴파일된 모듈에서 지원 됩니다.


[GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 절:

- AVG, COUNT, COUNT_BIG, MIN, MAX 및 SUM 집계 함수  

- MIN 및 MAX는 nvarchar, char, varchar, varchar, varbinary 및 binary 형식에 대해 지원되지 않습니다.  

[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md) 절:


- **ORDER BY** 절에서는 **DISTINCT** 가 지원되지 않습니다.


- ORDER BY 목록의 식이 GROUP BY 목록에 정확하게 나타나는 경우 [GROUP BY&#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)에서 지원됩니다.
  - 예를 들어, GROUP BY a + b ORDER BY a + b는 지원되지만 GROUP BY a, b ORDER BY a + b는 지원되지 않습니다.  


HAVING 절:

- WHERE 절과 동일한 식 제한 사항이 적용됩니다.


#### <a name="order-by-and-top-are-supported-in-natively-compiled-modules-with-some-restrictions"></a>ORDER BY 및 TOP은 고유하게 컴파일된 모듈에서 지원되며, 다음과 같은 몇 가지 제한이 적용됩니다.


- **WITH TIES** 절에서는 **PERCENT** 또는 **TOP** 가 지원되지 않습니다.


- **ORDER BY** 절에서는 **DISTINCT** 가 지원되지 않습니다.  


- **TOP** 절에서 상수를 사용할 때 **ORDER BY** 과 **TOP** 를 함께 사용할 경우 8,192개 이상은 지원되지 않습니다.
  - 쿼리에 조인 또는 집계 함수가 포함되어 있으면 이 제한이 더 낮아질 수 있습니다. 예를 들어, 조인이 하나 있고 테이블이 두 개 있으면 4,096개의 행으로 제한되고, 조인이 두 개 있고 테이블이 세 개 있으면 2,730개의 행으로 제한됩니다.  
  - 변수에 행 수를 저장하여 8,192개 이상의 결과를 가져올 수 있습니다.  

```tsql
DECLARE @v INT = 9000;
SELECT TOP (@v) … FROM … ORDER BY …
```

하지만 **TOP** 절에 상수를 사용하면 변수를 사용할 때보다 나은 성능을 가져옵니다.  

고유하게 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 대한 이러한 제한 사항은 메모리 액세스에 최적화된 테이블에 대한 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에는 적용되지 않습니다.  


##  <a name="dml"></a> 데이터 수정  

다음의 DML 문이 지원됩니다.  

-   INSERT VALUES(문당 하나의 행) 및 INSERT ... SELECT  

-   UPDATE  

-   DELETE  

-   WHERE은 UPDATE 및 DELETE 문에서 지원됩니다.  

##  <a name="cof"></a> 흐름 제어 언어  
 다음의 흐름 제어 언어 구문이 지원됩니다.  

-   [IF...ELSE&#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  

-   [WHILE&#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  

-   [RETURN&#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)  

-   [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)은 모든 [메모리 내 OLTP에 지원되는 데이터 형식](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) 및 메모리 액세스에 최적화된 테이블 형식을 사용합니다. 변수는 NULL 또는 NOT NULL로 선언할 수 있습니다.  

-   [SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  

-   [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  

               To achieve optimal performance, use a single TRY/CATCH block for an entire natively compiled T-SQL module.  

-   [THROW&#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  

-   BEGIN ATOMIC(저장 프로시저의 외부 수준). 자세한 내용은 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)을 참조하세요.  

##  <a name="so"></a> 지원되는 연산자  
 지원되는 연산자는 다음과 같습니다.  

-   [비교 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)(예: >, \<, >=, <=)  

-   단항 연산자(+, -).  

-   이항 연산자(*, /, +, -, %(모듈로))  

               The plus operator (+) is supported on both numbers and strings.  

-   논리 연산자(AND, OR, NOT).  

-   비트 연산자 ~, &, | 및 ^  

-   APPLY 연산자
    - **Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
      [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1부터 APPLY 연산자는 고유하게 컴파일된 모듈에서 지원됩니다.

##  <a name="bfncsp"></a> 고유하게 컴파일된 모듈의 기본 제공 함수  
 다음 함수는 메모리 액세스에 최적화된 테이블에 대한 제약 조건과 고유하게 컴파일된 T-SQL 모듈에서 지원됩니다.  

-   모든 [수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  

-   날짜 함수: CURRENT_TIMESTAMP, DATEADD, DATEDIFF, DATEFROMPARTS, DATEPART, DATETIME2FROMPARTS, DATETIMEFROMPARTS, DAY, EOMONTH, GETDATE, GETUTCDATE, MONTH, SMALLDATETIMEFROMPARTS, SYSDATETIME, SYSUTCDATETIME 및 YEAR  

-   문자열 함수: LEN, LTRIM, RTRIM 및 SUBSTRING  
    - **Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
      [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1부터 TRIM, TRANSLATE, CONCAT_WS 등의 기본 제공 함수도 지원됩니다.  

-   ID 함수: SCOPE_IDENTITY  

-   NULL 함수: ISNULL  

-   Uniqueidentifier 함수: NEWID 및 NEWSEQUENTIALID  

-   JSON 함수  
    - **Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
      [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1부터 JSON 함수는 고유하게 컴파일된 모듈에서 지원됩니다.

-   오류 함수: ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY 및 ERROR_STATE  

-   시스템 함수: @@rowcount 고유하게 컴파일된 저장 프로시저 내의 문은 @@rowcount를 업데이트합니다. 고유하게 컴파일된 저장 프로시저에서 @@rowcount를 사용하여 고유하게 컴파일된 저장 프로시저 내에서 실행된 마지막 문의 영향을 받는 행의 수를 확인할 수 있습니다. 그러나 @@rowcount는 고유하게 컴파일된 저장 프로시저의 실행이 시작될 때와 끝날 때 0으로 다시 설정됩니다.  

-   보안 기능: IS_MEMBER({'group' | 'role'}), IS_ROLEMEMBER ('role' [, 'database_principal']), IS_SRVROLEMEMBER ('role' [, 'login']), ORIGINAL_LOGIN(), SESSION_USER, CURRENT_USER, SUSER_ID(['login']), SUSER_SID(['login'] [, Param2]), SUSER_SNAME([server_user_sid]), SYSTEM_USER, SUSER_NAME, USER, USER_ID(['user']), USER_NAME([id]), CONTEXT_INFO()

-   네이티브 모듈의 실행을 중첩할 수 있습니다.

##  <a name="auditing"></a> 감사  
 프로시저 수준 감사는 고유하게 컴파일된 저장 프로시저에서 지원됩니다.  

 감사에 대한 자세한 내용은 [Create a Server Audit and Database Audit Specification](../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)를 참조하세요.  

##  <a name="tqh"></a> 테이블 및 쿼리 힌트  
 다음 항목이 지원됩니다.  

-   테이블 힌트 구문 또는 쿼리의 [OPTION 절&#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)에 있는 INDEX, FORCESCAN 및 FORCESEEK 힌트. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  

-   FORCE ORDER  

-   LOOP JOIN 힌트  

-   OPTIMIZE FOR  

 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  

##  <a name="los"></a> 정렬의 제한 사항  
 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) 및 [ORDER BY 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)을 사용하는 쿼리에서는 8,000개 이상의 행을 정렬할 수 있습니다. 하지만 [ORDER BY 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)이 없을 경우, [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)은 최대 8,000개까지만 행을 정렬할 수 있습니다. 조인이 있으면 이러한 행 수가 더 줄어듭니다.  

 쿼리에서 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) 연산자와 [ORDER BY 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)을 모두 사용하는 경우 TOP 연산자에 대해 최대 8192행을 지정할 수 있습니다. 8192행보다 더 많이 지정하면 다음 오류 메시지가 나타납니다. **메시지 41398, 수준 16, 상태 1, 프로시저 *\<procedureName>*, 줄 *\<lineNumber>* TOP 연산자는 최대 8192개의 행을 반환할 수 있습니다. *\<number>*개가 요청되었습니다.**  

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

 8192 행 제한은 `TOP N`에만 적용됩니다. 여기서 `N`은 앞의 예와 같이 상수입니다.  8192보다 큰 `N` 이 필요한 경우 값을 변수에 할당하고 이 변수를 `TOP`과 함께 사용할 수 있습니다.  

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

## <a name="see-also"></a>관련 항목:  
 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)   
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  



