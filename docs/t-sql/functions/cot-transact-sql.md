---
title: COT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COT_TSQL
- COT
dev_langs:
- TSQL
helpviewer_keywords:
- COT function
- cotangent
ms.assetid: c87a9dac-e398-4125-80c3-7df3c2ce6b63
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 080b20e15242342e9662b5b4c459a9e8160822ab
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="cot-transact-sql"></a>COT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정 된에서 라디안으로 지정된 된 각도의 삼각 코탄젠트를 반환 하는 수학 함수의 **float** 식입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COT ( float_expression )  
```  
  
## <a name="arguments"></a>인수  
*float_expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md)형식의 **float** 또는 암시적으로 변환할 수 있는 형식의 **float**합니다.
  
## <a name="return-types"></a>반환 형식
**float**
  
## <a name="examples"></a>예  
다음 예에서는 지정한 각도에 대해 COT를 반환합니다.
  
```sql
DECLARE @angle float;  
SET @angle = 124.1332;  
SELECT 'The COT of the angle is: ' + CONVERT(varchar,COT(@angle));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The COT of the angle is: -0.040312                
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  


