---
title: '*=(곱하기 대입)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '*=_TSQL'
- '*='
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, *=
- assignment operators, *=
- augmented operators, *=
- '*= (multiply equals)'
- '*= (multiplication assignment)'
ms.assetid: 816ff5dc-9a40-4c07-8351-39c194dbc079
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6ad2f4cd1c650831415eb4fea8182eaf5fb81fe
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68122085"
---
# <a name="-multiplication-assignment-transact-sql"></a>*=(곱하기 대입)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

두 숫자를 곱하고 값을 연산 결과로 설정합니다. 예를 들어 @x 변수가 35일 경우 @x *= 2는 원래 값 @x에서 2를 곱하고 @x를 새 값(70)으로 설정합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression *= expression  
```  
  
## <a name="arguments"></a>인수  
_expression_  
숫자 범주에서 [bit](../../t-sql/language-elements/expressions-transact-sql.md) 형식을 제외한 모든 유효한 데이터 형식 **expression**입니다.  
  
## <a name="result-types"></a>결과 형식  
우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
자세한 내용은 [&#42;&#40;곱하기&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/multiply-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
[연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
