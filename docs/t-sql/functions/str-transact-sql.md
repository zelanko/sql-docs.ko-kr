---
description: STR(Transact-SQL)
title: STR(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STR
- STR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d46fefcd37227bc3045e515d0160a373825aa409
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484145"
---
# <a name="str-transact-sql"></a>STR(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  숫자 데이터에서 변환된 문자 데이터를 반환합니다. 문자 데이터는 지정된 길이와 소수 자릿수를 사용하여 오른쪽에 맞춰집니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *float_expression*  
 소수점이 있는 근사치(**float**) 데이터 형식의 식입니다.  
  
 *length*  
 총 길이입니다. 소수점, 부호, 숫자 및 공백을 포함한 길이입니다. 기본값은 10입니다.  
  
 *decimal*  
 소수 자릿수(소수점 오른쪽의 자릿수)입니다. *decimal* 은 16보다 작거나 같아야 합니다. *decimal* 이 16보다 크면 결과는 소수점 오른쪽의 16자리까지로 잘립니다.  
  
## <a name="return-types"></a>반환 형식  
 **varchar**  
  
## <a name="remarks"></a>설명  
 STR에 대한 *length* 및 *decimal* 매개 변수가 제공되는 경우 해당 값은 양수여야 합니다. 숫자는 기본적으로 또는 decimal 매개 변수가 0인 경우 정수로 반올림됩니다. 지정된 길이는 소수점 앞의 숫자 부분과 숫자 부호(있는 경우)를 더한 것보다 크거나 같아야 합니다. 짧은 *float_expression* 은 지정된 길이에서 오른쪽 정렬되며 긴 *float_expression* 은 지정된 십진 자릿수에서 잘립니다. 예를 들어 STR(12, 10)의 결과는 12가 됩니다. 이는 결과 집합에서 오른쪽 정렬됩니다. 그러나 STR(1223, 2)은 결과 집합을 \*\*로 자릅니다. 문자열 함수는 중첩될 수 있습니다.  
  
> [!NOTE]  
>  유니코드 데이터로 변환하려면 CONVERT 또는 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 변환 함수에서 STR를 사용합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 다섯 자리의 숫자와 소수점으로 구성된 식을 여섯 자리 문자열로 변환합니다. 숫자의 소수 부분은 소수 첫째 자리로 반올림됩니다.  
  
```sql
SELECT STR(123.45, 6, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------  
 123.5  
  
(1 row(s) affected)  
```  
  
 식이 지정한 길이를 초과하면 문자열이 지정된 길이만큼 `**`를 반환합니다.  
  
```sql
SELECT STR(123.45, 2, 2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--  
**  
  
(1 row(s) affected)  
```  
  
 숫자 데이터가 `STR` 내에서 중첩되어도 결과는 지정된 형식의 문자 데이터입니다.  
  
```sql
SELECT STR (FLOOR (123.45), 8, 3);
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [형식 &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

