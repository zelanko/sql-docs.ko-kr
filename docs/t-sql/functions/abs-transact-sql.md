---
description: ABS(Transact-SQL)
title: ABS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ABS_TSQL
- ABS
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], positive
- values [SQL Server], absolute
- ABS function
- absolute positive value
ms.assetid: e2ea7a6d-3e2f-472c-afbc-437d3b835c03
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc1b312febf7f9718f7a6b2737d25e7a638577eb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472174"
---
# <a name="abs-transact-sql"></a>ABS(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

지정한 수식의 절대(양수) 값을 반환하는 수치 연산 함수입니다. (`ABS`는 음수 값을 양수 값으로 변경합니다. `ABS`는 0 또는 양수 값에 영향을 미치지 않습니다.)
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ABS ( numeric_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*numeric_expression*  
정밀 숫자 또는 근사 숫자 데이터 형식 범주의 식입니다.
  
## <a name="return-types"></a>반환 형식  
*numeric_expression* 과 같은 유형을 반환합니다.
  
## <a name="examples"></a>예제  
이 예에서는 3가지의 다른 숫자에 `ABS` 함수를 사용한 결과를 보여줍니다.
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---- ---- ----  
1.0  .0   1.0  
```  
  
`ABS` 함수가 수의 절대값이 지정된 데이터 형식으로 나타낼 수 있는 최대 수를 초과하면 오버플로 오류가 발생할 수 있습니다. 예를 들어 `int` 데이터 형식은 `-2,147,483,648`에서 `2,147,483,647`의 값 범위를 갖습니다. 부호 있는 정수 `-2,147,483,648`에 대한 절대값을 계산하면 이 절대값이 `int` 데이터 형식의 양수 범위 제한을 초과하기 때문에 오버플로 오류가 발생합니다.
  
```sql
DECLARE @i INT;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
이 오류 메시지를 반환합니다.
  
"메시지 8115, 수준 16, 상태 2, 줄 3"
  
"식을(를) 데이터 형식 int(으)로 변환하는 중 산술 오버플로 오류가 발생했습니다."

  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[기본 제공 함수s&#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

