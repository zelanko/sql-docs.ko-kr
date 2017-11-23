---
title: STUFF (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STUFF
- STUFF_TSQL
dev_langs: TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: db5876abd95b4eb9b21d91deeeb6bc0f1a242303
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="stuff-transact-sql"></a>STUFF(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  STUFF 함수는 다른 문자열에 문자열을 삽입합니다. 이 함수는 지정된 시작 위치와 문자 수에 따라 첫 번째 문자열의 문자를 삭제하고 두 번째 문자열을 시작 위치에 삽입합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 데이터입니다. *character_expression* 상수, 변수 또는 문자 또는 이진 데이터의 열 수 있습니다.  
  
 *시작*  
 삭제 및 삽입 시작 위치를 지정하는 정수 값입니다. 경우 *시작* 가 음수 또는 0 이면 null 문자열이 반환 됩니다. 경우 *시작* 첫 번째 보다 긴 *character_expression*, null 문자열이 반환 됩니다. *시작* 유형일 수 **bigint**합니다.  
  
 *length*  
 삭제할 문자 수를 지정하는 정수입니다. 경우 *길이* 가 음수 이면 null 문자열이 반환 됩니다. 경우 *길이* 첫 번째 보다 긴 *character_expression*, 문자까지 삭제 마지막으로 다음 시간이 내의 *character_expression*합니다.  경우 *길이* 삽입 문자열의 첫 번째 문자가 앞에 오는 0이 됩니다. *길이* 유형일 수 **bigint**합니다.

 *replaceWith_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 데이터입니다. *character_expression* 상수, 변수 또는 문자 또는 이진 데이터의 열 수 있습니다. 이 식은 대체 *길이* 자의 *character_expression* 에서 시작 *시작*합니다. 제공 `NULL` 로 *replaceWith_expression*, 아무 것도 삽입 하지 않고 문자를 제거 합니다.   
  
## <a name="return-types"></a>반환 형식  
 경우 문자 데이터를 반환 *character_expression* 지원 되는 문자 데이터 형식 중 하나입니다. 경우에 이진 데이터를 반환 *character_expression* 지원 되는 이진 데이터 형식 중 하나입니다.  
  
## <a name="remarks"></a>주의  
 시작 위치 또는 길이가 음수이거나 시작 위치가 첫 번째 문자열의 길이를 넘어서면 null 문자열이 반환됩니다. 시작 위치가 0일 경우 Null 값이 반환됩니다. 삭제할 길이가 첫 번째 문자열보다 길면 첫 번째 문자열의 첫 번째 문자까지 삭제됩니다.  

결과 값이 반환 유형이 지원하는 최대값보다 크면 오류가 발생합니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 SC 데이터 정렬을 사용 하는 경우 둘 다 *character_expression* 및 *replaceWith_expression* 서로게이트 쌍을 포함할 수 있습니다. 각 서로게이트를 계산 하는 길이 매개 변수 *character_expression* 는 단일 문자입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 첫 문자열 `abcdef`에서 `2` 위치의 `b`부터 세 문자를 삭제하고 삭제 지점에 두 번째 문자열을 삽입하여 만든 문자열을 반환합니다.  
  
```  
SELECT STUFF('abcdef', 2, 3, 'ijklmn');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
aijklmnef   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
