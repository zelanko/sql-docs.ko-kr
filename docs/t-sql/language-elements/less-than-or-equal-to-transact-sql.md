---
description: '&lt;=(작거나 같음)(Transact-SQL)'
title: '&lt;=(작거나 같음)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- <=
- Less
- Equal To
- <=_TSQL
- Less Than
- Equal
dev_langs:
- TSQL
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 1f05474c-0377-48cb-b567-9d85d0c40479
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c87bb7838242422ebcc76f7fd54e187234460b2e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466144"
---
# <a name="lt-less-than-or-equal-to-transact-sql"></a>&lt;=(작거나 같음)(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  두 식을 비교합니다(비교 연산자). Null  이 아닌 식을 비교하는 경우 왼쪽 피연산자의 값이 오른쪽 피연산자의 값보다 작거나 같으면 결과는 TRUE이고 그렇지 않으면 결과는 FALSE입니다.  
  
 =(등가) 비교 연산자와 달리 두 NULL 값에 대한 >= 비교의 결과는 ANSI_NULLS 설정에 따라 달라지지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
expression <= expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 두 식은 모두 암시적으로 변환 가능한 데이터 형식이어야 합니다. 변환은 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md) 규칙에 따라 달라집니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="examples"></a>예제  
  
### <a name="a-using--in-a-simple-query"></a>A. 간단한 쿼리에서 <= 사용  
 다음 예에서는 `HumanResources.Department` 테이블에서 `DepartmentID`의 값이 3보다 작거나 같은 모든 행을 반환합니다.  
  
```sql  
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
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
