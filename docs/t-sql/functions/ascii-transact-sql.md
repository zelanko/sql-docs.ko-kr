---
title: ASCII (Transact SQL) | Microsoft Docs
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
- ASCII_TSQL
- ASCII
dev_langs:
- TSQL
helpviewer_keywords:
- ASCII function
- characters [SQL Server], ASCII
- code [SQL Server], ASCII
- leftmost character of expression
ms.assetid: 45c2044a-0593-4805-8bae-0fad4bde2e6b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b933f33b8eb6b3909eaf7cb0afcd8bfe19862dee
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="ascii-transact-sql"></a>ASCII(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

문자 식에서 가장 왼쪽 문자의 ASCII 코드 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
ASCII ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
*character_expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 형식의 **char** 또는 **varchar**합니다.
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>주의
ASCII 정보 교환에 대 한 미국 표준 코드에 대 한 약어는 합니다. 이 컴퓨터에서 사용 되는 표준 인코딩 문자입니다. 목록이 ASCII 문자에 대 한 참조는 **인쇄 가능한 문자** 섹션 [ASCII](https://www.wikipedia.org/wiki/ASCII)합니다.

## <a name="examples"></a>예  
다음 예에서는 ASCII 문자 집합을 가정 하 고 반환 된 `ASCII` 6 자에 대 한 값입니다.
  
```sql
SELECT ASCII('A') AS A, ASCII('B') AS B,   
ASCII('a') AS a, ASCII('b') AS b,  
ASCII(1) AS [1], ASCII(2) AS [2];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
A           B           a           b           1           2  
----------- ----------- ----------- ----------- ----------- -----------  
65          66          97          98          49          50  
```  
  
## <a name="see-also"></a>참고 항목
 [CHAR &#40; Transact SQL &#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR &#40; Transact SQL &#41;](../../t-sql/functions/nchar-transact-sql.md)  
 [유니코드 &#40; Transact SQL &#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  


