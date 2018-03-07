---
title: "% = (나머지 할당) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '%=_TSQL'
- '%='
dev_langs:
- TSQL
helpviewer_keywords:
- '%= (modulo equals)'
- '%= (modulus assignment)'
- compound operators, %=
- assignment operators, %=
- augmented operators, %=
ms.assetid: 45e35516-1f4c-406b-a580-70a14b087847
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 064b586b1e6bbf10828ce7dfa1f8d759e5201e85
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="-modulus-assignment-transact-sql"></a>% = (나머지 할당) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  한 숫자를 다른 숫자로 나누고 값을 연산 결과로 설정합니다. 예를 들어 변수 @x 38 이며, 다음 equals @x % = 5는 원래 값의 @x5로 나누고 설정 @x (3)이 나누기의 나머지 부분에서 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression %= expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 의 유형 중 하나는 데이터를 제외 하 고 숫자 범주는 **비트** 데이터 형식입니다.  
  
## <a name="result-types"></a>결과 형식  
 우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>주의  
 자세한 내용은 참조 [% &#40; 모듈러스 &#41; &#40; Transact SQL &#41; ](../../t-sql/language-elements/modulo-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목:  
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
