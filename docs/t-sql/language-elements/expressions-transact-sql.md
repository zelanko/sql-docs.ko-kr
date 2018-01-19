---
title: "식 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- Boolean expressions
- expressions [SQL Server], about expressions
- combining expressions
- Transact-SQL expressions
- expressions [SQL Server], combining
- simple expressions [SQL Server]
- complex expressions [SQL Server]
ms.assetid: ee53c5c8-e36c-40f9-8cd1-d933791b98fa
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ab2d66c986bb5b4b34eaf74b4d65dbcb9fcfdd16
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="expressions-transact-sql"></a>식(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 단일 데이터 값을 얻기 위해 평가하는 기호와 연산자 조합입니다. 단순 식으로는 단일 상수, 변수, 열 또는 스칼라 함수가 있습니다. 연산자를 사용하면 두 개 이상의 단순 식을 결합하여 복합 식으로 만들 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
{ constant | scalar_function | [ table_name. ] column | variable   
    | ( expression ) | ( scalar_subquery )   
    | { unary_operator } expression   
    | expression { binary_operator } expression   
    | ranking_windowed_function | aggregate_windowed_function  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Expression in a SELECT statement  
<expression> ::=   
{  
    constant   
    | scalar_function   
    | column  
    | variable  
    | ( expression  )  
    | { unary_operator } expression   
    | expression { binary_operator } expression   
}  
[ COLLATE Windows_collation_name ]  
  
-- Scalar Expression in a DECLARE, SET, IF…ELSE, or WHILE statement  
<scalar_expression> ::=  
{  
    constant   
    | scalar_function   
    | variable  
    | ( expression  )  
    | (scalar_subquery )  
    | { unary_operator } expression   
    | expression { binary_operator } expression   
}  
[ COLLATE { Windows_collation_name ]  
  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|----------|----------------|  
|*constant*|특정한 단일 데이터 값을 나타내는 기호입니다. 자세한 내용은 참조 [상수 &#40; Transact SQL &#41; ](../../t-sql/data-types/constants-transact-sql.md).|  
|*scalar_function*|단위는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 특정 서비스를 제공 하 고 단일 값을 반환 하는 구문입니다. *스칼라 함수* SUM, GETDATE, CAST 함수, 스칼라 사용자 정의 함수 등의 기본 제공 스칼라 함수 일 수 있습니다.|  
|[ *table_name***.** ]|테이블의 이름 또는 별칭입니다.|  
|*column*|열의 이름입니다. 식에는 열 이름만 사용할 수 있습니다.|  
|*variable*|변수 또는 매개 변수의 이름입니다. 자세한 내용은 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)을 참조하세요.|  
|**(** *expression*  **)**|이 항목에서 정의된 바와 같이 유효한 식입니다. 괄호는 안에 있는 식의 모든 연산자를 평가한 후에 그 결과를 다른 식과 결합하는 그룹 연산자입니다.|  
|**(** *scalar_subquery* **)**|한 개의 값을 반환하는 하위 쿼리입니다. 예를 들어<br /><br /> `SELECT MAX(UnitPrice)`<br /><br /> `FROM Products`|  
|{ *unary_operator* }|단항 연산자는 숫자 데이터 형식 범주의 데이터 형식 하나로 평가되는 식에 대해서만 적용할 수 있습니다. 단 하나의 숫자 피연산자만 있는 연산자입니다.<br /><br /> +는 양수를 나타냅니다.<br /><br /> -는 음수를 나타냅니다.<br /><br /> ~는 보수 연산자를 나타냅니다.|  
|{ *binary_operator* }|두 식을 결합하여 단일 결과를 만드는 방식을 정의하는 연산자입니다. *binary_operator* 산술 연산자, 대입 연산자 (=), 비트 연산자, 비교 연산자, 논리 연산자, 문자열 연결 연산자 (+) 또는 단항 연산자 일 수 있습니다. 연산자에 대 한 자세한 내용은 참조 [연산자 &#40; Transact SQL &#41; ](../../t-sql/language-elements/operators-transact-sql.md).|  
|*ranking_windowed_function*|[!INCLUDE[tsql](../../includes/tsql-md.md)] 순위 함수입니다. 자세한 내용은 참조 [순위 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/ranking-functions-transact-sql.md).|  
|*aggregate_windowed_function*|OVER 절을 사용하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 집계 함수입니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).|  
  
## <a name="expression-results"></a>식 결과  
 단일 상수, 변수, 스칼라 함수, 열 이름, 데이터 정렬, 전체 자릿수, 소수 자릿수 및 식의 값으로 이루어진 단순 식은 데이터 형식, 데이터 정렬, 전체 자릿수, 소수 자릿수 및 참조된 요소의 값입니다.  
  
 결과 데이터 형식이 부울이 고 값은 다음 중 하나를 비교 연산자나 논리 연산자를 사용 하 여 두 식을 결합 하는 경우: TRUE, FALSE 또는 UNKNOWN입니다. Boolean 데이터 형식에 대 한 자세한 내용은 참조 [비교 연산자 &#40; Transact SQL &#41; ](../../t-sql/language-elements/comparison-operators-transact-sql.md).  
  
 산술, 비트 또는 문자열 연산자를 사용하여 두 식을 결합하면 연산자에 따라 결과 데이터 형식이 결정됩니다.  
  
 복합 식은 많은 기호로 구성되며 연산자는 단일 값의 결과로 평가됩니다. 결과 식의 데이터 형식, 데이터 정렬, 전체 자릿수 및 값은 최종 결과에 도달할 때까지 한 번에 두 개씩 구성 요소 식을 결합하여 결정됩니다. 식이 결합되는 순서는 식의 연산자 우선 순위에 따라 정의됩니다.  
  
## <a name="remarks"></a>주의  
 두 식이 모두 연산자가 지원하는 데이터 형식을 갖고 있으며 다음 조건 중 최소한 하나가 참인 경우에는 연산자로 두 식을 결합할 수 있습니다.  
  
-   식의 데이터 형식이 동일한 경우  
  
-   우선 순위가 낮은 데이터 형식이 우선 순위가 높은 데이터 형식으로 암시적으로 변환될 수 있는 경우  
  
 식이 이러한 조건을 만족하지 않으면 CAST 또는 CONVERT 함수를 사용하여 명시적으로 우선 순위가 낮은 데이터 형식을 우선 순위가 높은 데이터 형식으로 변환하거나 중간 데이터 형식으로 변환한 후 암시적으로 우선 순위가 높은 데이터 형식으로 변환할 수 있습니다.  
  
 지원되는 명시적 변환 또는 암시적 변환이 없는 경우에는 두 식을 결합할 수 없습니다.  
  
 문자열로 평가되는 모든 식의 데이터 정렬은 선행 정렬 규칙에 따라 설정됩니다. 자세한 내용은 참조 [데이터 정렬 선행 규칙 &#40; Transact SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
 C와 같은 프로그래밍 언어에서 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], 식은 항상 단일 결과를 계산 합니다. 식에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 선택 목록의 변형 규칙: 식은 결과 집합의 각 행에 대해 개별적으로 계산 됩니다. 단일 식은 결과 집합의 각 행에 서로 다른 값을 가질 수 있습니다. 그러나 각 행은 식에 대해 단 하나의 값만을 가집니다. 예를 들어 다음 `SELECT` 문에서 `ProductID`에 대한 참조와 선택 목록의 `1+2` 항목은 모두 식입니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, 1+2  
FROM Production.Product;  
GO  
```  
  
 `1+2` 식은 결과 집합의 각 행에서 `3`으로 평가됩니다. `ProductID` 식이 각 결과 집합 행에서 고유한 값을 생성하더라도 각 행은 `ProductID`에 대해 단 하나의 값을 가집니다.  
  
## <a name="see-also"></a>관련 항목:  
 [표준 시간대 &AMP;#40; Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [대/소문자 &#40; Transact SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CAST 및 CONVERT &#40;TRANSACT-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [COALESCE &#40; Transact SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [데이터 형식 우선 순위 &#40; Transact SQL &#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [NULLIF &#40; Transact SQL &#41;](../../t-sql/language-elements/nullif-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
