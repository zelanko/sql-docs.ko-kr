---
title: TRY_CONVERT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_CONVERT_TSQL
- TRY_CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CONVERT function
ms.assetid: 3e6e7825-6482-4cb2-a8c2-9abc99e265a6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8c66c7e7d91f754203d4f23b0d7f45a391aaec67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65946887"
---
# <a name="tryconvert-transact-sql"></a>TRY_CONVERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  캐스트에 성공하면 지정한 데이터 형식으로 캐스팅된 값을 반환합니다. 그렇지 않으면 Null을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
TRY_CONVERT ( data_type [ ( length ) ], expression [, style ] )  
```  
  
## <a name="arguments"></a>인수  
 *data_type [ ( length ) ]*  
 *expression*을 캐스팅할 데이터 형식입니다.  
  
 *expression*  
 캐스팅할 값입니다.  
  
 *style*  
 **TRY_CONVERT** 함수가 *expression*을 변환하는 방법을 지정하는 선택적 정수 식입니다.  
  
 *style*은 **CONVERT** 함수의 *style* 매개 변수와 동일한 값을 허용합니다. 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.  
  
 허용되는 값 범위는 *data_type* 값에 따라 결정됩니다. *style*이 Null이면 **TRY_CONVERT**는 Null을 반환합니다.  
  
## <a name="return-types"></a>반환 형식  
 캐스트에 성공하면 지정한 데이터 형식으로 캐스팅된 값을 반환합니다. 그렇지 않으면 Null을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 **TRY_CONVERT** 함수는 전달된 값을 사용하여 지정된 *data_type*으로 변환을 시도합니다. 캐스팅에 성공하면 **TRY_CONVERT**는 지정된 *data_type*으로 값을 반환합니다. 오류가 발생하면 Null이 반환됩니다. 그러나 명시적으로 허용되지 않는 변환을 요청하면 오류와 함께 **TRY_CONVERT**가 실패합니다.  
  
 **TRY_CONVERT**는 호환성 수준 110 이상의 예약 키워드입니다.  
  
 이 함수는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전이 설치되어 있는 서버에 대해서는 원격으로 실행할 수 있지만 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전 버전이 설치되어 있는 서버에 대해서는 원격으로 실행할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-tryconvert-returns-null"></a>1\. TRY_CONVERT가 Null 반환  
 다음 예에서는 캐스팅을 실패할 때 TRY_CONVERT가 null을 반환하는 것을 보여 줍니다.  
  
```sql  
SELECT   
    CASE WHEN TRY_CONVERT(float, 'test') IS NULL   
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
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-tryconvert-fails-with-an-error"></a>2\. TRY_CONVERT가 오류와 함께 실패  
 다음 예에서는 캐스팅이 명시적으로 허용되지 않은 경우 TRY_CONVERT가 오류를 반환하는 것을 보여 줍니다.  
  
```sql  
SELECT TRY_CONVERT(xml, 4) AS Result;  
GO  
```  
  
 정수는 xml 데이터 형식으로 캐스팅될 수 없으므로 이 문을 실행하면 오류가 발생합니다.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-tryconvert-succeeds"></a>C. TRY_CONVERT가 성공  
 이 예에서는 식이 해당 형식에 맞아야 한다는 것을 보여 줍니다.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
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
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
