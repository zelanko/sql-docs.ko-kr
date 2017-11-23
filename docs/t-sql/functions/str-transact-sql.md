---
title: STR (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- STR
- STR_TSQL
dev_langs: TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: d8792951add2462067bc21ed22ef1e5ce005c0f0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="str-transact-sql"></a>STR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  숫자 데이터에서 변환된 문자 데이터를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *float_expression*  
 근사 숫자 식 (**float**) 소수점이 있는 데이터 형식입니다.  
  
 *length*  
 총 길이입니다. 소수점, 부호, 숫자 및 공백을 포함한 길이입니다. 기본값은 10입니다.  
  
 *decimal*  
 소수 자릿수(소수점 오른쪽의 자릿수)입니다. *10 진수* 16 보다 작거나 같아야 합니다. 경우 *10 진수* 16 보다 크면 다음 결과가 소수점의 오른쪽에 16 자릿수에서 잘립니다.  
  
## <a name="return-types"></a>반환 형식  
 **varchar**  
  
## <a name="remarks"></a>주의  
 에 대 한 값을 제공 하는 경우 *길이* 및 *10 진수* str 매개 변수는 양수 여야 합니다. 숫자는 기본적으로 또는 decimal 매개 변수가 0인 경우 정수로 반올림됩니다. 지정된 길이는 소수점 앞의 숫자 부분과 숫자 부호(있는 경우)를 더한 것보다 크거나 같아야 합니다. 짧은 *float_expression* 는 long 및 지정된 된 길이에서 오른쪽 정렬 *float_expression* 소수 자릿수로 지정된 된 수로 잘립니다. 예를 들어 STR (12**,**10) 12는 결과 생성 합니다. 이는 결과 집합에서 오른쪽 정렬됩니다. 그러나 STR (1223**,**2) 결과 집합을 자릅니다 * *입니다. 문자열 함수를 중첩할 수 있습니다.  
  
> [!NOTE]  
>  유니코드 데이터를 변환 하려면 CONVERT STR를 사용 하거나 [캐스트](../../t-sql/functions/cast-and-convert-transact-sql.md) 변환 함수입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 다섯 자리의 숫자와 소수점으로 구성된 식을 여섯 자리 문자열로 변환합니다. 숫자의 소수 부분은 소수 첫째 자리로 반올림됩니다.  
  
```  
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
  
```  
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
  
```  
SELECT STR (FLOOR (123.45), 8, 3;)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

