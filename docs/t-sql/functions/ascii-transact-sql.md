---
title: ASCII(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4add8a1a63572e6e86d659c29ea29d172545b9e0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43076178"
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
**char** 또는 **varchar** 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>Remarks
ASCII는 **A**merican **S**tandard **C**ode for **I**nformation **I**nterchange를 나타냅니다. 최신 컴퓨터에 대한 문자 인코딩 표준으로 사용합니다. ASCII 문자 목록은 [ASCII](https://www.wikipedia.org/wiki/ASCII)의 **인쇄 가능 문자** 섹션을 참조하세요.

## <a name="examples"></a>예  
이 예에서는 대상 문자열이 ASCII 문자 집합을 사용함을 전제로 하여 6개 문자에 대한 `ASCII` 값을 반환합니다.
  
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
  
## <a name="see-also"></a>관련 항목:
 [CHAR&#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR&#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)  
 [UNICODE&#40;Transact-SQL&#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  


