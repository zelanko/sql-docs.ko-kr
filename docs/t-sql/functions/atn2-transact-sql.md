---
title: ATN2 (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ATN2
- ATN2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- arctangent
- tangent
- ATN2 function
ms.assetid: 014b291e-7cd7-4c39-b20d-5db3a9f0505d
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 3c68b65c2bde2d8b4c5cd8f34452563b433c6a29
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="atn2-transact-sql"></a>ATN2(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

원점에서 점 (y, x)까지의 광선과 양의 X축 사이의 각도(라디안)를 반환합니다. 여기서 x와 y는 지정한 두 float 식의 값입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
ATN2 ( float_expression , float_expression )  
```  
  
## <a name="arguments"></a>인수  
*float_expression* 는 [식](../../t-sql/language-elements/expressions-transact-sql.md) 의 **float** 데이터 형식입니다.
  
## <a name="return-types"></a>반환 형식
**float**
  
## <a name="examples"></a>예  
다음 예에서는 지정된 `ATN2` 및 `x` 요소에 대한 `y` 값을 계산합니다.
  
```sql
DECLARE @x float = 35.175643, @y float = 129.44;  
SELECT 'The ATN2 of the angle is: ' + CONVERT(varchar,ATN2(@x,@y ));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The ATN2 of the angle is: 0.265345                         
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[float 및 real &#40; Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
[수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  


