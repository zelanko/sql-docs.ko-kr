---
title: "&gt;=(크거나 같음)(Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
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
- Greater
- '>='
- '>= (Greater Than or Equal To)'
- Equal To
- '>=_TSQL'
- Greater Than
- Equal
dev_langs:
- TSQL
helpviewer_keywords:
- greater than or equal to operator (>=)
- '>= (greater than or equal to operator)'
ms.assetid: 641ee28d-7536-46dd-a48a-6c63c2d59278
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1e8888629e0aefae619dacef1934a24d06922473
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="gt-greater-than-or-equal-to-transact-sql"></a>&gt;=(크거나 같음)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  한 식이 다른 한 식보다 크거나 같은지 비교합니다(비교 연산자).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression >= expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 두 식은 모두 암시적으로 변환 가능한 데이터 형식이어야 합니다. 변환은 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md) 규칙에 따라 달라집니다.  
  
## <a name="result-types"></a>결과 형식  
 Boolean  
  
## <a name="remarks"></a>Remarks  
 Null이 아닌 식을 비교하는 경우 왼쪽 피연산자의 값이 오른쪽 피연산자의 값보다 크거나 같으면 결과는 TRUE이고 그렇지 않으면 결과는 FALSE입니다.  
  
 =(등가)  비교 연산자와 달리 두 NULL  값에 대한 >=  비교의 결과는 ANSI_NULLS  설정에 따라 달라지지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using--in-a-simple-query"></a>1. 간단한 쿼리에서 >= 사용  
 다음 예에서는 `HumanResources.Department` 테이블에서 `DepartmentID`의 값이 13보다 큰 모든 행을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID >= 13  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
13           Quality Assurance  
14           Facilities and Maintenance  
15           Shipping and Receiving  
16           Executive  
  
(4 row(s) affected)  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [=&#40;같음&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/equals-transact-sql.md)   
 [&#62;&#40;보다 큼&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
