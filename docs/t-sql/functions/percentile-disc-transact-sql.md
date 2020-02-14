---
title: PERCENTILE_DISC(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ccd04bec4416fdf5bb5f2137dc2f86e69a9a2ab4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67914341"
---
# <a name="percentile_disc-transact-sql"></a>PERCENTILE_DISC(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 전체 행 집합에 정렬된 값 또는 행 집합의 고유 파티션 내에 정렬된 값의 특정 백분위수를 계산합니다. 지정된 백분위수 값 *P*에 대해 PERCENTILE_DISC는 ORDER BY 절의 식 값을 정렬합니다. *P*보다 크거나 같은 가장 작은 지정된 CUME_DIST 값(동일한 정렬 사양 기준)을 반환합니다. 예를 들어 PERCENTILE_DISC (0.5)는 식의 50번째 백분위수(즉, 중앙값)를 컴퓨팅합니다. PERCENTILE_DISC는 열 값의 불연속 분포를 기반으로 백분위수를 계산합니다. 결과는 열의 특정 값과 같습니다.  
  
 ![아티클 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>인수  
 *literal*  
 계산할 백분위수입니다. 값은 0.0에서 1.0 사이여야 합니다.  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC)**  
 정렬할 값 목록을 지정하고 백분위수를 컴퓨팅합니다. *order_by_expression*은 하나만 허용됩니다. 기본 정렬 순서는 오름차순입니다. 값 목록은 정렬 조작에 유효한 모든 데이터 형식일 수 있습니다.  
  
 OVER **(** \<partition_by_clause>)**  
 FROM 절의 결과 집합을 파티션으로 분할합니다. Percentile 함수는 해당 파티션에 적용됩니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요. \<ORDER BY 절> 및 \<rows 또는 range 절>은 PERCENTILE_DISC 함수에 지정할 수 없습니다.  
  
## <a name="return-types"></a>반환 형식  
 반환 형식은 *order_by_expression* 형식에 의해 결정됩니다.  
  
## <a name="compatibility-support"></a>호환성 지원  
 호환성 수준 110 이상에서 WITHIN GROUP은 예약 키워드입니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 모든 null은 데이터 집합에서 무시됩니다.  
  
 PERCENTILE_DISC는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="basic-syntax-example"></a>기본 구문 예제  

 다음 예에서는 PERCENTILE_CONT 및 PERCENTILE_DISC를 사용하여 각 부서의 직원 급여 중앙값을 찾습니다. 이 함수는 같은 값을 반환하지 않을 수 있습니다.
* PERCENTILE_CONT는 데이터 집합에 존재하지 않는 경우에도 적절한 값을 반환합니다.
* PERCENTILE_DISC는 실제 설정된 값을 반환합니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="basic-syntax-example"></a>기본 구문 예제  

 다음 예에서는 PERCENTILE_CONT 및 PERCENTILE_DISC를 사용하여 각 부서의 직원 급여 중앙값을 찾습니다. 이 함수는 같은 값을 반환하지 않을 수 있습니다.
* PERCENTILE_CONT는 데이터 집합에 존재하지 않는 경우에도 적절한 값을 반환합니다. 
* PERCENTILE_DISC는 실제 설정된 값을 반환합니다.  
  
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
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>참고 항목  
 [PERCENTILE_CONT&#40;Transact-SQL&#41;](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  


