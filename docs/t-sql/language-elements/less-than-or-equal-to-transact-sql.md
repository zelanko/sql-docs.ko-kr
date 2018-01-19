---
title: "&lt;= (작거나 같음) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- <=
- Less
- Equal To
- <=_TSQL
- Less Than
- Equal
dev_langs: TSQL
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 1f05474c-0377-48cb-b567-9d85d0c40479
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a330768916e0b57db1e11258cd124fb486174cf9
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="lt-less-than-or-equal-to-transact-sql"></a>&lt;= (작거나 같음) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 식을 비교합니다(비교 연산자).   Null  이 아닌 식을 비교하는 경우 왼쪽 피연산자의 값이 오른쪽 피연산자의 값보다 작거나 같으면 결과는 TRUE이고 그렇지 않으면 결과는 FALSE입니다.  
  
 =(등가)  비교 연산자와 달리 두 NULL  값에 대한 >=  비교의 결과는 ANSI_NULLS  설정에 따라 달라지지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression <= expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다. 두 식은 모두 암시적으로 변환 가능한 데이터 형식이어야 합니다. 변환의 규칙에 따라 달라 집니다 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md)합니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="examples"></a>예  
  
### <a name="a-using--in-a-simple-query"></a>1. 사용 하 여 < 간단한 쿼리에서 =  
 다음 예에서는 `HumanResources.Department` 테이블에서 `DepartmentID`의 값이 3보다 작거나 같은 모든 행을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID <= 3  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
1            Engineering  
2            Tool Design  
3            Sales  
  
(3 row(s) affected)  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
