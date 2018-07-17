---
title: PERCENTILE_CONT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PERCENTILE_CONT_TSQL
- PERCENTILE_CONT
dev_langs:
- TSQL
helpviewer_keywords:
- analytic functions, PERCENTILE_CONT
- PERCENTILE_CONT function
ms.assetid: d019419e-5297-4994-97d5-e9c8fc61bbf4
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7462c57a98f3b60cff64f71478456e18256e290f
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781964"
---
# <a name="percentilecont-transact-sql"></a>PERCENTILE_CONT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 열 값의 연속 분포를 기반으로 백분위수를 계산합니다. 결과는 보간되며 열의 특정 값과 같지 않을 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
PERCENTILE_CONT ( numeric_literal )   
    WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>인수  
 *numeric_literal*  
 계산할 백분위수입니다. 값은 0.0에서 1.0 사이여야 합니다.  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC ]**)**  
 정렬할 숫자 값 목록을 지정하고 백분위수를 계산합니다. *order_by_expression*은 하나만 허용됩니다. 식은 정확한 숫자 형식(**int**, **bigint**, **smallint**, **tinyint**, **numeric**, **bit**, **decimal**, **smallmoney**, **money**) 또는 적절한 숫자 형식(**float**, **real**)이어야 합니다. 다른 데이터 형식은 허용되지 않습니다. 기본 정렬 순서는 오름차순입니다.  
  
 OVER **(** \<partition_by_clause> **)**  
 FROM 절이 생성한 결과 집합을 백분위수 함수가 적용되는 파티션으로 나눕니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요. OVER 구문의 \<ORDER BY 절> 및 \<rows 또는 range 절>은 PERCENTILE_CONT 함수에 지정할 수 없습니다.  
  
## <a name="return-types"></a>반환 형식  
 **float(53)**  
  
## <a name="compatibility-support"></a>호환성 지원  
 호환성 수준 110 이상에서 WITHIN GROUP은 예약 키워드입니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 모든 null은 데이터 집합에서 무시됩니다.  
  
 PERCENTILE_CONT는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-basic-syntax-example"></a>1. 기본 구문 예제  
 다음 예에서는 PERCENTILE_CONT 및 PERCENTILE_DISC를 사용하여 각 부서에서 직원 급여의 중앙값을 찾습니다. 이러한 함수는 같은 값을 반환하지 않을 수 있습니다. 이는 PERCENTILE_CONT는 데이터 집합에 있는지 여부에 관계없이 적절한 값을 보간하는 반면, PERCENTILE_DISC는 항상 해당 집합에서 실제 값을 반환하기 때문입니다.  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 다음은 결과 집합의 일부입니다.  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-basic-syntax-example"></a>2. 기본 구문 예제  
 다음 예에서는 PERCENTILE_CONT 및 PERCENTILE_DISC를 사용하여 각 부서에서 직원 급여의 중앙값을 찾습니다. 이러한 함수는 같은 값을 반환하지 않을 수 있습니다. 이는 PERCENTILE_CONT는 데이터 집합에 있는지 여부에 관계없이 적절한 값을 보간하는 반면, PERCENTILE_DISC는 항상 해당 집합에서 실제 값을 반환하기 때문입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
    OVER (PARTITION BY DepartmentName) AS MedianCont  
,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
    OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 다음은 결과 집합의 일부입니다.  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.826900    16.8269
Engineering            34.375000    32.6923
Human Resources        17.427850    16.5865
Shipping and Receiving 9.250000      9.0000
```  
  
## <a name="see-also"></a>참고 항목  
 [PERCENTILE_DISC&#40;Transact-SQL&#41;](../../t-sql/functions/percentile-disc-transact-sql.md)  
  
  


