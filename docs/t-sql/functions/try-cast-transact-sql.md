---
title: TRY_CAST (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09c5b6060798f28541f61e763954ed44920cf83d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
 캐스팅할 데이터 형식 *식*합니다.  
  
 *length*  
 대상 데이터 형식의 길이를 지정하는 선택적 정수입니다.  
  
 허용 되는 값의 범위 값에 의해 결정 됩니다 *data_type*합니다.  
  
## <a name="return-types"></a>반환 형식  
 캐스트에 성공하면 지정한 데이터 형식으로 캐스팅된 값을 반환합니다. 그렇지 않으면 Null을 반환합니다.  
  
## <a name="remarks"></a>주의  
 **TRY_CAST** 는 전달 된 값을 사용 하 고 지정 된 변환 하려고 *data_type*합니다. 캐스팅에 성공 하면 **TRY_CAST** 지정 된 값을 반환 *data_type*; 오류가 발생 하면 null이 반환 됩니다. 그러나 명시적으로 허용 되지 않는, 다음 변환을 요청 하는 경우 **TRY_CAST** 오류가 발생 하면서 실패 합니다.  
  
 **TRY_CAST** 새 예약된 된 키워드 아니며 모든 호환성 수준에서 모두 사용할 수는 있습니다. **TRY_CAST** 동일한 의미 체계에 **TRY_CONVERT** 원격 서버에 연결할 때.  
  
## <a name="examples"></a>예  
  
### <a name="a-trycast-returns-null"></a>1. TRY_CAST가 null을 반환  
 다음 예에서는 캐스팅을 실패할 때 TRY_CAST가 null을 반환하는 것을 보여 줍니다.  
  
```tsql  
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
  
```tsql  
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
  
### <a name="b-trycast-fails-with-an-error"></a>2. TRY_CAST가 오류와 함께 실패  
 다음 예에서는 캐스팅이 명시적으로 허용되지 않은 경우 TRY_CAST가 오류를 반환하는 것을 보여 줍니다.  
  
```tsql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 정수는 xml 데이터 형식으로 캐스팅될 수 없으므로 이 문을 실행하면 오류가 발생합니다.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-trycast-succeeds"></a>3. TRY_CAST 성공  
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
  
## <a name="see-also"></a>관련 항목:  
 [TRY_CONVERT &#40; Transact SQL &#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

