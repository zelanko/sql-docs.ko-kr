---
title: 식(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Boolean expressions
- expressions [SQL Server], about expressions
- combining expressions
- Transact-SQL expressions
- expressions [SQL Server], combining
- simple expressions [SQL Server]
- complex expressions [SQL Server]
ms.assetid: ee53c5c8-e36c-40f9-8cd1-d933791b98fa
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55e3dda77a2b623ef50fe64ad82824b84a934f44
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124103"
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
  
-- Scalar Expression in a DECLARE, SET, IF...ELSE, or WHILE statement  
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
|*constant*|특정한 단일 데이터 값을 나타내는 기호입니다. 자세한 내용은 [상수&#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)을 참조하세요.|  
|*scalar_function*|특정 서비스를 제공하고 단일 값을 반환하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문의 단위입니다. *scalar_function*은 SUM, GETDATE 또는 CAST 함수 또는 스칼라 사용자 정의 함수와 같은 기본 제공 스칼라 함수가 될 수 있습니다.|  
|[ _table_name_**.** ]|테이블의 이름 또는 별칭입니다.|  
|*column*|열의 이름입니다. 식에는 열 이름만 사용할 수 있습니다.|  
|*variable*|변수 또는 매개 변수의 이름입니다. 자세한 내용은 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)을 참조하세요.|  
|**(** _expression_  **)**|이 항목에서 정의된 바와 같이 유효한 식입니다. 괄호는 안에 있는 식의 모든 연산자를 평가한 후에 그 결과를 다른 식과 결합하는 그룹 연산자입니다.|  
|**(** _scalar_subquery_ **)**|한 개의 값을 반환하는 하위 쿼리입니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> `SELECT MAX(UnitPrice)`<br /><br /> `FROM Products`|  
|{ *unary_operator* }|단항 연산자는 숫자 데이터 형식 범주의 데이터 형식 하나로 평가되는 식에 대해서만 적용할 수 있습니다. 단 하나의 숫자 피연산자만 있는 연산자입니다.<br /><br /> +는 양수를 나타냅니다.<br /><br /> -는 음수를 나타냅니다.<br /><br /> ~는 보수 연산자를 나타냅니다.|  
|{ *binary_operator* }|두 식을 결합하여 단일 결과를 만드는 방식을 정의하는 연산자입니다. *binary_operator*는 산술 연산자, 대입 연산자(=), 비트 연산자, 비교 연산자, 논리 연산자, 문자열 연결 연산자(+) 또는 단항 연산자일 수 있습니다. 연산자에 대한 자세한 내용은 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)를 참조하세요.|  
|*ranking_windowed_function*|[!INCLUDE[tsql](../../includes/tsql-md.md)] 순위 함수입니다. 자세한 내용은 [순위 함수&#40;Transact-SQL&#41;](../../t-sql/functions/ranking-functions-transact-sql.md)를 참조하세요.|  
|*aggregate_windowed_function*|OVER 절을 사용하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 집계 함수입니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.|  
  
## <a name="expression-results"></a>식 결과  
 단일 상수, 변수, 스칼라 함수, 열 이름, 데이터 정렬, 전체 자릿수, 소수 자릿수 및 식의 값으로 이루어진 단순 식은 데이터 형식, 데이터 정렬, 전체 자릿수, 소수 자릿수 및 참조된 요소의 값입니다.  
  
 비교 연산자나 논리 연산자를 사용하여 두 식을 결합하면 결과 데이터 형식은 부울이 되며 값은 TRUE, FALSE 또는 UNKNOWN 중 하나가 됩니다. 부울 데이터 형식에 대한 자세한 내용은 [비교 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)를 참조하세요.  
  
 산술, 비트 또는 문자열 연산자를 사용하여 두 식을 결합하면 연산자에 따라 결과 데이터 형식이 결정됩니다.  
  
 복합 식은 많은 기호로 구성되며 연산자는 단일 값의 결과로 평가됩니다. 결과 식의 데이터 형식, 데이터 정렬, 전체 자릿수 및 값은 최종 결과에 도달할 때까지 한 번에 두 개씩 구성 요소 식을 결합하여 결정됩니다. 식이 결합되는 순서는 식의 연산자 우선 순위에 따라 정의됩니다.  
  
## <a name="remarks"></a>Remarks  
 두 식이 모두 연산자가 지원하는 데이터 형식을 갖고 있으며 다음 조건 중 최소한 하나가 참인 경우에는 연산자로 두 식을 결합할 수 있습니다.  
  
-   식의 데이터 형식이 동일한 경우  
  
-   우선 순위가 낮은 데이터 형식이 우선 순위가 높은 데이터 형식으로 암시적으로 변환될 수 있는 경우  
  
 식이 이러한 조건을 만족하지 않으면 CAST 또는 CONVERT 함수를 사용하여 명시적으로 우선 순위가 낮은 데이터 형식을 우선 순위가 높은 데이터 형식으로 변환하거나 중간 데이터 형식으로 변환한 후 암시적으로 우선 순위가 높은 데이터 형식으로 변환할 수 있습니다.  
  
 지원되는 명시적 변환 또는 암시적 변환이 없는 경우에는 두 식을 결합할 수 없습니다.  
  
 문자열로 평가되는 모든 식의 데이터 정렬은 선행 정렬 규칙에 따라 설정됩니다. 자세한 내용은 [데이터 정렬 선행 규칙&#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)을 참조하세요.  
  
 C 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]과 같은 프로그래밍 언어에서 식은 항상 단일 결과로 평가됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 선택 목록의 식은 이 규칙이 적용되지 않습니다. 식은 결과 집합의 각 행에 대해 개별적으로 평가됩니다. 단일 식은 결과 집합의 각 행에 서로 다른 값을 가질 수 있습니다. 그러나 각 행은 식에 대해 단 하나의 값만을 가집니다. 예를 들어 다음 `SELECT` 문에서 `ProductID`에 대한 참조와 선택 목록의 `1+2` 항목은 모두 식입니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, 1+2  
FROM Production.Product;  
GO  
```  
  
 `1+2` 식은 결과 집합의 각 행에서 `3`으로 평가됩니다. `ProductID` 식이 각 결과 집합 행에서 고유한 값을 생성하더라도 각 행은 `ProductID`에 대해 단 하나의 값을 가집니다.  
  
## <a name="see-also"></a>참고 항목  
 [AT TIME ZONE&#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [COALESCE&#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [데이터 형식 변환&#40;Database Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [NULLIF&#40;Transact-SQL&#41;](../../t-sql/language-elements/nullif-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
