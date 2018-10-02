---
title: '&lt;&gt;(같지 않음)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- <>
- <>_TSQL
- Not Equal To
- Not Equal
- <>(Not Equal To)
- NOT
- Equal
dev_langs:
- TSQL
helpviewer_keywords:
- not equal to operator (<>)
- <> (not equal to operator)
ms.assetid: 34cf9b38-d589-4be9-925a-116e224609a0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0850c14d67ee64c18b8e44a26e74bab4ab45a4fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47760311"
---
# <a name="not-equal-to-transact-sql---traditional"></a>같지 않음(Transact SQL) - 기존
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 식을 비교합니다(비교 연산자).   Null이 아닌 식을 비교하는 경우 왼쪽 피연산자가 오른쪽 피연산자와 같지 않으면 결과는 TRUE이고 그렇지 않으면 결과는 FALSE입니다.   피연산자 중 하나 또는 둘 다가 NULL이면 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md) 항목을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression <> expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 두 식은 모두 암시적으로 변환 가능한 데이터 형식이어야 합니다. 변환은 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md) 규칙에 따라 달라집니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="examples"></a>예  
  
### <a name="a-using--in-a-simple-query"></a>1. 간단한 쿼리에서 <> 사용  
 다음 예에서는 `Production.ProductCategory` 테이블에서 `ProductCategoryID`의 값이 3  또는 2가 아닌 모든 행을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductCategoryID, Name  
FROM Production.ProductCategory  
WHERE ProductCategoryID <> 3 AND ProductCategoryID <> 2;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductCategoryID Name  
----------------- --------------------------------------------------  
1                 Bikes  
4                 Accessories  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비교 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)  
  
  
