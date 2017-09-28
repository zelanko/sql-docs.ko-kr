---
title: ACOS (Transact SQL) | Microsoft Docs
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
- ACOS
- ACOS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cosine
- ACOS function
- arccosine
ms.assetid: 4ec6b46e-9438-4f0f-8b96-461edd84280a
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aad94e57120771babeb734c7410fdcac94c28c21
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="acos-transact-sql"></a>ACOS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

코사인이 지정 된 라디안 단위로 각도 반환 하는 수학 함수의 **float** 식; 아크코사인 값을 호출된 합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
ACOS ( float_expression )  
```  
  
## <a name="arguments"></a>인수  
*float_expression*  
형식의 식 **float** 또는 암시적으로 변환할 수 있는 형식의 **float**, 값이 1부터 1 까지입니다. 값이 이 범위를 벗어나면 NULL이 반환되고 도메인 오류가 보고됩니다.
  
## <a name="return-types"></a>반환 형식  
**float**
  
## <a name="examples"></a>예  
다음 예에서는 지정한 수의 ACOS을 반환합니다.
  
```sql
SET NOCOUNT OFF;  
DECLARE @cos float;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(varchar, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
### <a name="includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 

다음 예에서는 지정한 수의 ACOS을 반환합니다.
  
```sql
DECLARE @cos float;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(varchar, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[함수](../../t-sql/functions/functions.md)
  
  


