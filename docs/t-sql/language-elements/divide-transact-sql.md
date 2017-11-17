---
title: "(나누기) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /
- /_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- / (divide)
- division [SQL Server]
- divide operator (/)
ms.assetid: 1d69893b-e5c3-441d-8dd8-0e5eb872ecfc
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e3e8a94a92ca592ce6a2deb5d13915606f04f984
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="divide-transact-sql"></a>(나누기) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  숫자를 다른 숫자로 나눕니다(산술 나누기 연산자).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
dividend / divisor  
```  
  
## <a name="arguments"></a>인수  
 *dividend*  
 나눌 숫자 식입니다. *피제수* 든 사용할 수 [식](../../t-sql/language-elements/expressions-transact-sql.md) 숫자 값의 데이터 형식 중 하나를 제외 하 고 데이터 형식 범주에서는 **datetime** 및 **smalldatetime** 데이터 형식입니다.  
  
 *divisor*  
 피제수를 나눌 숫자 식입니다. *divisor* 제외한 숫자 데이터 형식 범주의 데이터 형식 중 하나에 대 한 올바른 식일 수 있습니다는 **datetime** 및 **smalldatetime** 데이터 형식입니다.  
  
## <a name="result-types"></a>결과 형식  
 우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
 정수인 경우 *피제수* 정수 나눈 *제 수*, 결과 정수는 소수 부분이 잘린입니다.  
  
## <a name="remarks"></a>주의  
 / 연산자로 반환되는 실제 값은 첫째 식을 둘째 식으로 나누어 나온 몫입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 나누기 산술 연산자를 사용하여 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]의 영업 사원에 대한 월간 판매 목표를 계산합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT s.BusinessEntityID AS SalesPersonID, FirstName, LastName, SalesQuota, SalesQuota/12 AS 'Sales Target Per Month'  
FROM Sales.SalesPerson AS s   
JOIN HumanResources.Employee AS e   
    ON s.BusinessEntityID = e.BusinessEntityID  
JOIN Person.Person AS p   
    ON e.BusinessEntityID = p.BusinessEntityID;  
```  
  
 다음은 결과 집합의 일부입니다.  
  
```  
  
SalesPersonID FirstName    LastName          SalesQuota  Sales Target Per Month  
------------- ------------ ----------------- ----------- ------------------  
274           Stephen      Jiang             NULL        NULL  
275           Michael      Blythe            300000.00   25000.00  
276           Linda        Mitchell          250000.00   20833.3333  
277           Jillian      Carson            250000.00   20833.3333  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 나누기 산술 연산자를 사용 하 여 간단한 비율 병가 시간에 각 직원의 휴가 시간을 계산 하려면.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, VacationHours/SickLeaveHours AS PersonalTimeRatio  
FROM DimEmployee;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [&#40; 나누기 EQUALS &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



