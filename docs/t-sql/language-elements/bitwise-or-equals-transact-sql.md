---
title: "| = (비트 또는 할당) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/10/2017
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
- '|='
- '|=_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- compound operators, |=
- assignment operators, |=
- augmented operators, |=
- '|= (bitwise OR equals)'
ms.assetid: bd746a4f-6498-4196-bf2e-b6f457a15d44
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c5f991e93e9fd11e74e9284a6f85e1f010187bed
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="-bitwise-or-assignment-transact-sql"></a>| = (비트 또는 할당) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 이진 식으로 변환되는 두 개의 지정된 정수 값 간에 비트 논리 OR 연산을 수행하고 값을 연산 결과로 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression |= expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 의 유형 중 하나는 데이터를 제외 하 고 숫자 범주는 **비트** 데이터 형식입니다.  
  
## <a name="result-types"></a>결과 형식  
 우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>주의  
 자세한 내용은 참조 [&#124; &#40; 비트 OR &#41; &#40; Transact SQL &#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목:  
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
