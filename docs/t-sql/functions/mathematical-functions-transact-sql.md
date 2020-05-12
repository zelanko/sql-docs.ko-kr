---
title: 수치 연산 함수(Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 28cee5f6b7b1f3ea16ac490a24b10417d0d5f83d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822574"
---
# <a name="mathematical-functions-transact-sql"></a>수치 연산 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  다음 스칼라 함수는 일반적으로 인수에 의해 제공되는 입력 값을 기반으로 계산을 수행하고 숫자 값을 반환합니다.  
  
||||  
|-|-|-|  
|[ABS](../../t-sql/functions/abs-transact-sql.md)|[DEGREES](../../t-sql/functions/degrees-transact-sql.md)|[RAND](../../t-sql/functions/rand-transact-sql.md)|  
|[ACOS](../../t-sql/functions/acos-transact-sql.md)|[EXP](../../t-sql/functions/exp-transact-sql.md)|[ROUND](../../t-sql/functions/round-transact-sql.md)|  
|[ASIN](../../t-sql/functions/asin-transact-sql.md)|[FLOOR](../../t-sql/functions/floor-transact-sql.md)|[SIGN](../../t-sql/functions/sign-transact-sql.md)|  
|[ATAN](../../t-sql/functions/atan-transact-sql.md)|[LOG](../../t-sql/functions/log-transact-sql.md)|[SIN](../../t-sql/functions/sin-transact-sql.md)|  
|[ATN2](../../t-sql/functions/atn2-transact-sql.md)|[LOG10](../../t-sql/functions/log10-transact-sql.md)|[SQRT](../../t-sql/functions/sqrt-transact-sql.md)|  
|[CEILING](../../t-sql/functions/ceiling-transact-sql.md)|[PI](../../t-sql/functions/pi-transact-sql.md)|[SQUARE](../../t-sql/functions/square-transact-sql.md)|  
|[COS](../../t-sql/functions/cos-transact-sql.md)|[POWER](../../t-sql/functions/power-transact-sql.md)|[TAN](../../t-sql/functions/tan-transact-sql.md)|  
|[COT](../../t-sql/functions/cot-transact-sql.md)|[RADIANS](../../t-sql/functions/radians-transact-sql.md)||  
  
> [!NOTE]  
>  ABS, CEILING, DEGREES, FLOOR, POWER, RADIANS, SIGN 등의 산술 함수는 입력 값과 동일한 데이터 형식의 값을 반환합니다. EXP, LOG, LOG10, SQUARE, SQRT를 포함하여 삼각 함수 등의 기타 함수는 입력 값을 **float**으로 캐스팅하고 **float** 값을 반환합니다.  
  
 RAND를 제외한 모든 산술 함수는 결정적 함수입니다. 이는 지정된 입력 값 집합을 사용하여 호출할 때마다 동일한 결과를 반환함을 의미합니다. RAND는 초기값 매개 변수가 지정된 경우에만 결정적입니다. 함수 결정성에 대한 자세한 내용은 [결정적 함수 및 비결정적 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
  [산술 연산자 &#40;Transact-SQL&#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)  
  [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
