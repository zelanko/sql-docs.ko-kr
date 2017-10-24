---
title: "!&lt; (보다 작지 않음) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '!<'
- Not Less
- '!<_TSQL'
- Not Less Than
- Less Than
dev_langs:
- TSQL
helpviewer_keywords:
- '!< (not less than)'
- not less than operator (!<)
ms.assetid: ecbb598e-58a2-4b6c-90b4-3ad5bdfcae39
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 46933faa80e509bf2ed8f2e21fc9386113e9784a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lt-not-less-than-transact-sql"></a>!&lt; (보다 작지 않음) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  두 식을 비교합니다(비교 연산자).   Null이 아닌 식을 비교하는 경우 왼쪽 피연산자의 값이 오른쪽 피연산자의 값보다 작지 않으면 결과는 TRUE이고 그렇지 않으면 결과는 FALSE입니다. 항목을 참조 중 하나 또는 두 개의 피연산자가 NULL 이면 [SET ansi_nulls&#40; Transact SQL &#41; ](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
expression !< expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다. 두 식은 모두 암시적으로 변환 가능한 데이터 형식이어야 합니다. 변환의 규칙에 따라 달라 집니다 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md)합니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  

