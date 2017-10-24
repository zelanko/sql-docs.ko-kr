---
title: "- (빼기) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6f3013e03ddc1d7481c36be6ed8cce4cf4572c04
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="--subtract-transact-sql"></a>-(빼기)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 숫자를 빼는 빼기 산술 연산자입니다. 날짜에서 일 수를 뺄 수도 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression - expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 숫자 값의 데이터 형식 중 하나를 제외 하 고 데이터 형식 범주에서는 **비트** 데이터 형식입니다. 함께 사용할 수 없습니다 **날짜**, **시간**, **datetime2**, 또는 **datetimeoffset** 데이터 형식입니다.  
  
## <a name="result-types"></a>결과 형식  
 우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-subtraction-in-a-select-statement"></a>1. SELECT 문에서 빼기 사용  
 다음 예에서는 세율이 가장 높은 시/도와 세율이 가장 낮은 시/도 간의 세율 차를 계산합니다.  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT MAX(TaxRate) - MIN(TaxRate) AS 'Tax Rate Difference'  
FROM Sales.SalesTaxRate  
WHERE StateProvinceID IS NOT NULL;  
GO  
```  
  
 계산 순서를 변경하려면 괄호를 사용합니다. 괄호 안의 계산부터 먼저 수행됩니다. 괄호가 중첩되면 가장 안쪽에 있는 계산이 우선적으로 처리됩니다.  
  
### <a name="b-using-date-subtraction"></a>2. 날짜 빼기 사용  
 다음 예에서는 `datetime` 날짜에서 일 수를 뺍니다.  
  
 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
```  
-- Uses AdventureWorks  
  
DECLARE @altstartdate datetime;  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-subtraction-in-a-select-statement"></a>C: SELECT 문에서 빼기 사용  
 다음 예제에서 가장 높은 기본 숙박료가 직원과 가장 낮은 세율 인 직원 며 기본 숙박료가 차이 계산에서 `dimEmployee` 테이블입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT MAX(BaseRate) - MIN(BaseRate) AS BaseRateDifference  
FROM DimEmployee;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [산술 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)   
 [-&#40; 음수 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/unary-operators-negative.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [-= &#40; 빼기 EQUALS &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



