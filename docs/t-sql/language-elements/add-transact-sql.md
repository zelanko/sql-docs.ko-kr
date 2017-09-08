---
title: "+ (추가) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- add
- +
- +_TSQL
- + (Add)
dev_langs:
- TSQL
helpviewer_keywords:
- addition (+)
- adding numbers
- + (add)
- plus sign (+)
- add operator (+)
ms.assetid: 4ba8baac-5f07-432c-87c5-d23e7011da55
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1f23e9847250e6b899d990d3fdfeb710149b4c2d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="-add-transact-sql"></a>+(더하기)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 숫자를 더합니다. 이 더하기 산술 연산자를 사용하여 날짜에 일 수를 더할 수도 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
    
expression + expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 의 유형 중 하나는 데이터를 제외 하 고 숫자 범주는 **비트** 데이터 형식입니다. 함께 사용할 수 없습니다 **날짜**, **시간**, **datetime2**, 또는 **datetimeoffset** 데이터 형식입니다.  
  
## <a name="result-types"></a>결과 형식  
 우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-addition-operator-to-calculate-the-total-number-of-hours-away-from-work-for-each-employee"></a>1. 더하기 연산자를 사용하여 직원별 전체 휴무 시간 계산  
 이 예에서는 휴가 및 병가 시간 수가 계산 된 시간 수를 추가 하 여 각 직원에 대 한 휴무 시간 총 수를 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, VacationHours, SickLeaveHours,   
    VacationHours + SickLeaveHours AS 'Total Hours Away'  
FROM HumanResources.Employee AS e  
    JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
ORDER BY 'Total Hours Away' ASC;  
GO  
```  
  
### <a name="b-using-the-addition-operator-to-add-days-to-date-and-time-values"></a>2. 더하기 연산자를 사용하여 일 수를 날짜 및 시간 값에 더하기  
 일 수를 추가 하는이 예제는 `datetime` 날짜입니다.  
  
```  
  
SET NOCOUNT ON  
DECLARE @startdate datetime, @adddays int;  
SET @startdate = ''January 10, 1900 12:00 AM';  
SET @adddays = 5;  
SET NOCOUNT OFF;  
SELECT @startdate + 1.25 AS 'Start Date',   
   @startdate + @adddays AS 'Add Date';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Start Date                  Add Date`  
  
 `--------------------------- ---------------------------`  
  
 `1900-01-11 06:00:00.000     1900-01-15 00:00:00.000`  
  
 `(1 row(s) affected)`  
  
### <a name="c-adding-character-and-integer-data-types"></a>3. 문자와 정수 데이터 형식 더하기  
 다음 예제에서는 추가 **int** 데이터 형식 값과 문자 값을 문자 데이터 형식으로 변환 하 여 **int**합니다. 유효 하지 않은 문자에 있는 경우는 **char** 문자열의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 오류를 반환 합니다.  
  
```  
DECLARE @addvalue int;  
SET @addvalue = 15;  
SELECT '125127' + @addvalue;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `-----------------------`  
  
 `125142`  
  
 `(1 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-the-addition-operator-to-calculate-the-total-number-of-hours-away-from-work-for-each-employee"></a>더하기 연산자를 사용 하 여 각 직원에 대 한 휴무 시간 총 수를 계산 하는 d:  
 다음 예제에서는 휴가 및 병가 시간 수가 계산 된 시간 수를 추가 하 여 각 직원에 대 한 휴무 시간 총 개수를 검색 하 고 결과를 오름차순를 정렬 합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, VacationHours, SickLeaveHours,   
    VacationHours + SickLeaveHours AS TotalHoursAway  
FROM DimEmployee  
ORDER BY TotalHoursAway ASC;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [+ = &#40; 추가 EQUALS &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [CAST 및 convert&#40; Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  



