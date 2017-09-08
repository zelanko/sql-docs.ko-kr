---
title: "수치 연산 함수 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec4a6767acab606d6459b439683a88a0cae1caf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mathematical-functions-transact-sql"></a>수치 연산 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  다음 스칼라 함수는 일반적으로 인수에 의해 제공되는 입력 값을 기반으로 계산을 수행하고 숫자 값을 반환합니다.  
  
||||  
|-|-|-|  
|[ABS](../../t-sql/functions/abs-transact-sql.md)|[도](../../t-sql/functions/degrees-transact-sql.md)|[RAND](../../t-sql/functions/rand-transact-sql.md)|  
|[ACOS](../../t-sql/functions/acos-transact-sql.md)|[EXP](../../t-sql/functions/exp-transact-sql.md)|[반올림](../../t-sql/functions/round-transact-sql.md)|  
|[ASIN](../../t-sql/functions/asin-transact-sql.md)|[FLOOR](../../t-sql/functions/floor-transact-sql.md)|[로그인](../../t-sql/functions/sign-transact-sql.md)|  
|[ATAN](../../t-sql/functions/atan-transact-sql.md)|[로그](../../t-sql/functions/log-transact-sql.md)|[SIN](../../t-sql/functions/sin-transact-sql.md)|  
|[ATN2](../../t-sql/functions/atn2-transact-sql.md)|[LOG10](../../t-sql/functions/log10-transact-sql.md)|[SQRT](../../t-sql/functions/sqrt-transact-sql.md)|  
|[최대값](../../t-sql/functions/ceiling-transact-sql.md)|[PI](../../t-sql/functions/pi-transact-sql.md)|[사각형](../../t-sql/functions/square-transact-sql.md)|  
|[COS](../../t-sql/functions/cos-transact-sql.md)|[전원](../../t-sql/functions/power-transact-sql.md)|[TAN](../../t-sql/functions/tan-transact-sql.md)|  
|[COT](../../t-sql/functions/cot-transact-sql.md)|[라디안](../../t-sql/functions/radians-transact-sql.md)||  
  
> [!NOTE]  
>  ABS, CEILING, DEGREES, FLOOR, POWER, RADIANS, SIGN 등의 산술 함수는 입력 값과 동일한 데이터 형식의 값을 반환합니다. 삼각 및 다른 함수, EXP, 로그, LOG10, SQUARE 및 SQRT를 포함 하 여 해당 입력된 값을 캐스팅 **float** 다음 다시 돌아와 **float** 값입니다.  
  
 RAND를 제외한 모든 산술 함수는 결정적 함수입니다. 이는 지정된 입력 값 집합을 사용하여 호출할 때마다 동일한 결과를 반환함을 의미합니다. RAND는 초기값 매개 변수가 지정된 경우에만 결정적입니다. 함수 결정성에 대 한 자세한 내용은 참조 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
  [산술 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)  
  [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  

