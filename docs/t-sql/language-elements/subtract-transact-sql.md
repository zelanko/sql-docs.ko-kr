---
description: '- (빼기)(Transact-SQL)'
title: '- (빼기)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- subtract
- '-'
- -_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
- minus operator (-)
- subtracting numbers
ms.assetid: db23145f-f17d-4b90-be09-28a881cacd1a
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e8cc97df3b1a574e0ef7816d2b6cf44ee5288620
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466064"
---
# <a name="--subtraction-transact-sql"></a>-(빼기)(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  두 숫자를 빼는 빼기 산술 연산자입니다. 날짜에서 일 수를 뺄 수도 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
expression - expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 숫자 데이터 형식 범주에서 **bit** 데이터 형식을 제외한 모든 데이터 형식 중 하나로 된 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. **날짜**, **시간**, **datetime2** 또는 **datetimeoffset** 데이터 형식을 함께 사용할 수 없습니다.  
  
## <a name="result-types"></a>결과 형식  
 우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-subtraction-in-a-select-statement"></a>A. SELECT 문에서 빼기 사용  
 다음 예에서는 세율이 가장 높은 시/도와 세율이 가장 낮은 시/도 간의 세율 차를 계산합니다.  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
-- Uses AdventureWorks  
  
SELECT MAX(TaxRate) - MIN(TaxRate) AS 'Tax Rate Difference'  
FROM Sales.SalesTaxRate  
WHERE StateProvinceID IS NOT NULL;  
GO  
```  
  
 계산 순서를 변경하려면 괄호를 사용합니다. 괄호 안의 계산부터 먼저 수행됩니다. 괄호가 중첩되면 가장 안쪽에 있는 계산이 우선적으로 처리됩니다.  
  
### <a name="b-using-date-subtraction"></a>B. 날짜 빼기 사용  
 다음 예에서는 `datetime` 날짜에서 일 수를 뺍니다.  
  
 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @altstartdate DATETIME;  
SET @altstartdate = CONVERT(DATETIME, ''January 10, 1900 3:00 AM', 101);  
SELECT @altstartdate - 1.5 AS 'Subtract Date';  
```  
  
 결과 집합은 다음과 같습니다.  
  
 ```
 Subtract Date  
 -----------------------  
 1900-01-08 15:00:00.000  

 (1 row(s) affected)
 ```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-subtraction-in-a-select-statement"></a>C. SELECT 문에서 빼기 사용  
 다음 예는 `dimEmployee` 테이블에서 기본 급여가 가장 높은 직원과 세율이 가장 낮은 직원 간의 기본 급여 차이를 계산합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT MAX(BaseRate) - MIN(BaseRate) AS BaseRateDifference  
FROM DimEmployee;  
```  
  
## <a name="see-also"></a>참고 항목  
 [-=&#40;빼기 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
 [산술 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)   
 [-&#40;음수&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/unary-operators-negative.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
  
  


