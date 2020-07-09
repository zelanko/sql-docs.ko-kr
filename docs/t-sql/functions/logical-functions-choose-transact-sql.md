---
title: CHOOSE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHOOSE
- CHOOSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHOOSE function
ms.assetid: 1c382c83-7500-4bae-bbdc-c1dbebd3d83f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2c2894f44ca54d26c8a0a4392e91d052de3a55aa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784471"
---
# <a name="logical-functions---choose-transact-sql"></a>논리 함수 - CHOOSE(Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 값 목록에서 지정된 인덱스에 있는 항목을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
CHOOSE ( index, val_1, val_2 [, val_n ] )  
```  
  
## <a name="arguments"></a>인수  
 *index*  
 index 인수 다음에 나오는 항목 목록에 대한 1부터 시작하는 인덱스를 나타내는 정수 식입니다.  
  
 **int** 이외의 숫자 데이터 형식으로 된 인덱스 값을 제공할 경우 값이 암시적으로 정수로 변환됩니다. 인덱스 값이 값 배열 한계를 초과하면 CHOOSE는 Null을 반환합니다.  
  
 *val_1 ... val_n*  
 임의의 데이터 형식으로 된 쉼표로 구분된 값 목록입니다.  
  
## <a name="return-types"></a>반환 형식  
 함수에 전달된 형식 집합 중에서 우선 순위가 가장 높은 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
 CHOOSE는 배열에서 인덱스와 같은 역할을 하며 배열은 index 인수 다음에 나오는 인수로 구성됩니다. index 인수는 다음 중 반환될 값을 결정합니다.  
  
## <a name="examples"></a>예  

### <a name="a-simple-choose-example"></a>A. 간단한 CHOOSE 예제

 다음 예에서는 제공된 값 목록에서 세 번째 항목을 반환합니다.  
 
```  
SELECT CHOOSE ( 3, 'Manager', 'Director', 'Developer', 'Tester' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
-------------  
Developer  
  
(1 row(s) affected)  
```  

### <a name="b-simple-choose-example-based-on-column"></a>B. 열을 기반으로 하는 간단한 CHOOSE 예제

 다음 예제에서는 `ProductCategoryID` 열의 값에 따라 간단한 문자열을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductCategoryID, CHOOSE (ProductCategoryID, 'A','B','C','D','E') AS Expression1  
FROM Production.ProductCategory;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductCategoryID Expression1  
----------------- -----------  
3                 C  
1                 A  
2                 B  
4                 D  
  
(4 row(s) affected)  
  
```  

### <a name="c-choose-in-combination-with-month"></a>C. MONTH와 조합된 CHOOSE
  
 다음 예제에서는 직원이 고용된 시즌을 반환합니다. MONTH 함수는 `HireDate` 열에서 월 값을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, HireDate, CHOOSE(MONTH(HireDate),'Winter','Winter', 'Spring','Spring','Spring','Summer','Summer',   
                                                  'Summer','Autumn','Autumn','Autumn','Winter') AS Quarter_Hired  
FROM HumanResources.Employee  
WHERE  YEAR(HireDate) > 2005  
ORDER BY YEAR(HireDate);  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
JobTitle                                           HireDate   Quarter_Hired  
-------------------------------------------------- ---------- -------------  
Sales Representative                               2006-11-01 Autumn  
European Sales Manager                             2006-05-18 Spring  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2007-07-01 Summer  
Pacific Sales Manager                              2007-04-15 Spring  
Sales Representative                               2007-07-01 Summer  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [IIF &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)  
  
  
