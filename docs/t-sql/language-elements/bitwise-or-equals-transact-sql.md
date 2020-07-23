---
title: '|= (비트 OR)'
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '|='
- '|=_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, |=
- assignment operators, |=
- augmented operators, |=
- '|= (bitwise OR equals)'
ms.assetid: bd746a4f-6498-4196-bf2e-b6f457a15d44
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5fd9255bc39b041f97e60cd3f64f0416cf49ac31
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916255"
---
# <a name="-bitwise-or-assignment-transact-sql"></a>|= (비트 OR 대입)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 이진 식으로 변환되는 두 개의 지정된 정수 값 간에 비트 논리 OR 연산을 수행하고 값을 연산 결과로 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression |= expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 숫자 범주에서 **bit** 데이터 형식을 제외한 모든 데이터 형식 중 하나에 대한 올바른 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="result-types"></a>결과 형식  
 우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
 자세한 내용은 [&#124;&#40;비트 OR&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
