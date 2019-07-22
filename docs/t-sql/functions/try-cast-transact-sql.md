---
title: TRY_CAST(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 313f1bd13cf1b12a0685eeb101998792e0586767
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098776"
---
# <a name="trycast-transact-sql"></a>TRY_CAST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  캐스트에 성공하면 지정한 데이터 형식으로 캐스팅된 값을 반환합니다. 그렇지 않으면 Null을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 캐스팅할 값입니다. 유효한 식입니다.  
  
 *data_type*  
 *expression*을 캐스팅할 데이터 형식입니다.  
  
 *length*  
 대상 데이터 형식의 길이를 지정하는 선택적 정수입니다.  
  
 허용되는 값 범위는 *data_type* 값에 따라 결정됩니다.  
  
## <a name="return-types"></a>반환 형식  
 캐스트에 성공하면 지정한 데이터 형식으로 캐스팅된 값을 반환합니다. 그렇지 않으면 Null을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 **TRY_CAST** 함수는 전달된 값을 사용하여 지정된 *data_type*으로 변환하려고 시도합니다. 캐스팅에 성공하면 **TRY_CAST**는 지정된 *data_type*으로 값을 반환합니다. 오류가 발생하면 Null이 반환됩니다. 그러나 명시적으로 허용되지 않는 변환을 요청하면 오류와 함께 **TRY_CAST**가 실패합니다.  
  
 **TRY_CAST**는 예약 키워드가 아니며 모든 호환성 수준에서 사용할 수 있습니다. **TRY_CAST**는 원격 서버에 연결할 때 **TRY_CONVERT**와 동일한 의미 체계를 갖습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-trycast-returns-null"></a>1\. TRY_CAST가 null을 반환  
 다음 예에서는 캐스팅을 실패할 때 TRY_CAST가 null을 반환하는 것을 보여 줍니다.  
  
```sql  
SELECT   
    CASE WHEN TRY_CAST('test' AS float) IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 다음 예에서는 식이 해당 형식에 맞아야 한다는 것을 보여 줍니다.  
  
```sql  
SET DATEFORMAT dmy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-trycast-fails-with-an-error"></a>2\. TRY_CAST가 오류와 함께 실패  
 다음 예에서는 캐스팅이 명시적으로 허용되지 않은 경우 TRY_CAST가 오류를 반환하는 것을 보여 줍니다.  
  
```sql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 정수는 xml 데이터 형식으로 캐스팅될 수 없으므로 이 문을 실행하면 오류가 발생합니다.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-trycast-succeeds"></a>C. TRY_CAST 성공  
 이 예에서는 식이 해당 형식에 맞아야 한다는 것을 보여 줍니다.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [TRY_CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
